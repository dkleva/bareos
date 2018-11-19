.. _FiledConfChapter:

Client/File Daemon Configuration
================================


.. index:: 
   triple: General; Configuration; Client/File daemon
.. index:: General; Client/File daemon Configuration 

The Client (or File Daemon) Configuration is one of the simpler ones to
specify. Generally, other than changing the Client name so that error
messages are easily identified, you will not need to modify the default
Client configuration file.

For a general discussion of configuration file and resources including
the data types recognized by **Bareos**, please see the
:ref:`Configuration ConfigureChapter` chapter of this
manual. The following Client Resource definitions must be defined:

-  :ref:`Client ClientResourceClient` – to define what
   Clients are to be backed up.

-  :ref:`Director ClientResourceDirector` – to define the
   Director’s name and its access password.

-  :ref:`Messages MessagesChapter` – to define where
   error and information messages are to be sent.

.. _ClientResourceClient:

Client Resource
---------------


.. index:: 
   triple: General; Resource; Client
.. index:: General; Client Resource 

The Client Resource (or FileDaemon) resource defines the name of the
Client (as used by the Director) as well as the port on which the Client
listens for Director connections.

Start of the Client records. There must be one and only one Client
resource in the configuration file, since it defines the properties of
the current client program.

.. raw:: latex

   \defDirective{Fd}{Client}{Absolute Job Timeout}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Allow Bandwidth Bursting}{}{}{%
   This option sets if there is Bandwidth Limiting in effect if the limiting
   code can use bursting e.g. when from a certain timeslice not all bandwidth
   is used this bandwidth can be used in a next timeslice. Which mean you will
   get a smoother limiting which will be much closer to the actual limit set
   but it also means that sometimes the bandwidth will be above the setting here.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Allowed Job Command}{}{}{%
   This directive filters what type of jobs the filedaemon should allow.
   Until now we had the -b (backup only) and -r (restore only) flags which could
   be specified at the startup of the filedaemon.

   Allowed Job Command can be defined globally for all directors by
   adding it to the global filedaemon resource or for a specific director when
   added to the director resource.

   You specify all commands you want to be executed by the filedaemon. When you
   don't specify the option it will be empty which means all commands are allowed.

   The following example shows how to use this functionality:
   \bconfigInput{config/FdClientAllowedJobCommand1.conf}


   All commands that are allowed are specified each on a new line with the
   Allowed Job Command keyword.

   The following job commands are recognized:

   \begin{description}
       \item[backup] allow backups to be made
       \item[restore] allow restores to be done
       \item[verify] allow verify jobs to be done
       \item[estimate] allow estimate cmds to be executed
       \item[runscript] allow runscripts to run
   \end{description}

   Only the important commands the filedaemon can perform are filtered, as
   some commands are part of the above protocols and by disallowing
   the action the other commands are not invoked at all.

   If runscripts are not needed it would be recommended as a security measure to disable
   running those or only allow the commands that you really want to be used.

   Runscripts are particularly a problem as they allow the \bareosFd to run
   arbitrary commands. You may also look into the \linkResourceDirective{Fd}{Client}{Allowed Script Dir} keyword to
   limit the impact of the runscript command.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Allowed Script Dir}{}{}{%
   This directive limits the impact of the runscript command of the filedaemon.

   It can be specified either for all directors  by adding it to the global filedaemon resource
   or for a specific director when added to the director resource.

   All directories in which the scripts or commands are located
   that you allow to be run by the runscript command of the filedaemon. Any
   program not in one of these paths (or subpaths) cannot be used. The
   implementation checks if the full path of the script starts with one of the
   specified paths.

   The following example shows how to use this functionality:

   \bconfigInput{config/FdClientAllowedScriptDir1.conf}
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Always Use LMDB}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Compatible}{}{}{%
   This directive enables the compatible mode of the file daemon. In
   this mode the file daemon will try to be as compatible to a native
   Bacula file daemon as possible. Enabling this option means that
   certain new options available in Bareos cannot be used as they would
   lead to data not being able to be restored by a Native Bareos file daemon.

   The default value for this directive was changed from yes to no since Bareos \sinceVersion{fd}{Compatible = no}{15.2.0}.

   When you want to use bareos-only features, the value of compatible must be no.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{FD Address}{}{}{%
   This record is optional,  and if it is specified, it will cause the File
   daemon server (for  Director connections) to bind to the specified {\bf
   IP-Address},  which is either a domain name or an IP address specified as a
   dotted quadruple.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{FD Addresses}{}{}{%
   Specify the ports and addresses on which the File daemon listens for
   Director connections.  Probably the simplest way to explain is to show
   an example:

   \bconfigInput{config/FdClientFDAddresses1.conf}

   where ip, ip4, ip6, addr, and port are all keywords. Note, that  the address
   can be specified as either a dotted quadruple, or  IPv6 colon notation, or as
   a symbolic name (only in the ip specification).  Also, the port can be specified
   as a number or as the mnemonic value from  the /etc/services file.  If a port
   is not specified, the default will be used. If an ip  section is specified,
   the resolution can be made either by IPv4 or  IPv6. If ip4 is specified, then
   only IPv4 resolutions will be permitted,  and likewise with ip6.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{FD Port}{}{}{%
   This specifies the port number  on which the Client listens for Director
   connections. It must agree  with the FDPort specified in the Client resource
   of the Director's  configuration file.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{FD Source Address}{}{}{%
   If specified, the \bareosFd will bind to the specified address when creating outbound connections.
   If this record is not specified, the kernel will choose
   the best address according to the routing table (the default).
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Heartbeat Interval}{}{}{%
   This record defines an interval of time in seconds.  For each heartbeat that the
   File daemon receives from the Storage daemon, it will forward it to the
   Director.  In addition, if no heartbeat has been received from the
   Storage daemon and thus forwarded the File daemon will send a heartbeat
   signal to the Director and to the Storage daemon to keep the channels
   active.  Setting the interval to 0 (zero) disables the heartbeat.
   This feature is particularly useful if you have a router
   that does not follow Internet standards and times out a valid
   connection after a short duration despite the fact that keepalive is
   set. This usually results in a broken pipe error message.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{LMDB Threshold}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Maximum Bandwidth Per Job}{}{}{%
   The speed parameter specifies the maximum allowed bandwidth that a job may
   use.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Maximum Concurrent Jobs}{}{}{%
   This directive specifies the maximum number of Jobs that should run
   concurrently. Each contact from the Director (e.g. status request, job start
   request) is considered as a Job,
   so if you want to be able to do a \bcommand{status} request in the console
   at the same time as a Job is running, you
   will need to set this value greater than 1.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Maximum Network Buffer Size}{}{}{%
   This directive specifies the initial network buffer size to use.
   This size will be adjusted down if it is too large until it
   is accepted by the OS. Please use  care in setting this value since if it is
   too large, it will  be trimmed by 512 bytes until the OS is happy, which may
   require  a large number of system calls. The default value is 65,536 bytes.

   Note, on certain Windows machines, there are reports that the
   transfer rates are very slow and this seems to be related to
   the default 65,536 size. On systems where the transfer rates
   seem abnormally slow compared to other systems, you might try
   setting the Maximum Network Buffer Size to 32,768 in both the
   File daemon and in the Storage daemon.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Messages}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Name}{}{}{%
   The client name that must be used  by the Director when connecting. Generally,
   it is a good idea  to use a name related to the machine so that error messages
   can be easily identified if you have multiple Clients.  This directive is
   required.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pid Directory}{}{}{%
   This directive specifies a directory in which the File Daemon
   may put its process Id file files. The process Id file is used to  shutdown
   Bareos and to prevent multiple copies of  Bareos from running simultaneously.

   The Bareos file daemon uses a platform specific default value,
   that is defined at compile time.
   Typically on Linux systems, it is set to \path|/var/lib/bareos/| or \path|/var/run/|.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Cipher}{}{}{%
   See the \nameref{DataEncryption} chapter of this manual.

   Depending on the openssl library version different ciphers are available. To choose the desired cipher, you can use the PKI Cipher option in the filedaemon configuration. Note that you have to set \linkResourceDirective{Fd}{Client}{Compatible} = no:

   \bconfigInput{config/FdClientPki.conf}

   The available options (and ciphers) are:
   \begin{itemize}
       \item aes128
       \item aes192
       \item aes256
       \item camellia128
       \item camellia192
       \item camellia256
       \item aes128hmacsha1
       \item aes256hmacsha1
       \item blowfish
   \end{itemize}
   They depend on the version of the openssl library installed.

   For decryption of encrypted data, the right decompression algorithm should be automatically chosen.

   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Encryption}{}{}{%
   See \nameref{DataEncryption}.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Key Pair}{}{}{%
   See \nameref{DataEncryption}.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Master Key}{}{}{%
   See \nameref{DataEncryption}.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Signatures}{}{}{%
   See \nameref{DataEncryption}.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Pki Signer}{}{}{%
   See \nameref{DataEncryption}.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Plugin Directory}{}{}{%
   This directive specifies a directory in which the File Daemon searches for
   plugins with the name \file{<pluginname>-fd.so} which it will load at startup.
   Typically on Linux systems, plugins are installed to \path|/usr/lib/bareos/plugins/| or \path|/usr/lib64/bareos/plugins/|.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Plugin Names}{}{}{%
   If a \linkResourceDirective{Fd}{Client}{Plugin Directory} is specified
   \configdirective{Plugin Names} defines, which \nameref{fdPlugins} get loaded.

   If \configdirective{Plugin Names} is not defined, all plugins get loaded,
   otherwise the defined ones.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Scripts Directory}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{SD Connect Timeout}{}{}{%
   This  record defines an interval of time that  the File daemon will try to
   connect to the  Storage daemon. If no connection
   is made in the specified time interval, the File daemon  cancels the Job.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Sub Sys Directory}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Secure Erase Command}{}{}{%
   When files are no longer needed, Bareos will delete (unlink) them.
   With this directive, it will call the specified command to delete these files. See \nameref{sec:SecureEraseCommand} for details.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Authenticate}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS CA Certificate Dir}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS CA Certificate File}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Certificate}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Certificate Revocation List}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Enable}{}{}{%
   Bareos can be configured to encrypt all its network traffic. See chapter \nameref{TlsDirectives} to see how the Bareos Director (and the other components) have to be configured to use TLS.
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Key}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Require}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{TLS Verify Peer}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Ver Id}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Client}{Working Directory}{}{}{%
   This directive is optional and specifies a directory in which the File
   daemon  may put its status files.
   %\TODO{This directory should be used only by {\bf
   %Bareos}, but may be shared by other Bareos daemons provided the daemon
   %names on the {\bf Name} definition are unique for each daemon.}

   % The bareos file daemon uses a platform specific default value, that is defined at compile time.
   % For Linux systems, the default is \path|/var/lib/bareos/|.
   % For Windows systems it is \%TEMP\%.

   On Win32 systems, in some circumstances you may need to specify a drive
   letter in the specified working directory path.  Also, please be sure
   that this directory is writable by the SYSTEM user otherwise restores
   may fail (the bootstrap file that is transferred to the File daemon from
   the Director is temporarily put in this directory before being passed
   to the Storage daemon).
   }

The following is an example of a valid Client resource definition:

.. raw:: latex

   \footnotesize

::

    Client {                              # this is me
      Name = rufus-fd
    }

.. raw:: latex

   \normalsize

.. _ClientResourceDirector:

Director Resource
-----------------

.. index:: General; Director Resource 

.. index:: 
   triple: General; Resource; Director

The Director resource defines the name and password of the Directors
that are permitted to contact this Client.

.. raw:: latex

   \defDirective{Fd}{Director}{Address}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Allowed Job Command}{}{}{%
   see \linkResourceDirective{Fd}{Client}{Allowed Job Command}
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Allowed Script Dir}{}{}{%
   see \linkResourceDirective{Fd}{Client}{Allowed Script Dir}
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Connection From Client To Director}{}{}{%
   For details, see \nameref{sec:ClientInitiatedConnection}.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Connection From Director To Client}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Maximum Bandwidth Per Job}{}{}{%
   The speed parameter specifies the maximum allowed bandwidth that a job may use
   when started from this Director. The speed parameter should be specified in
   k/s, Kb/s, m/s or Mb/s.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Monitor}{}{}{%
   If Monitor is set to {\bf no},  this director will have full access
   to this Client. If Monitor is set to  {\bf yes}, this director will only be
   able to fetch the current status of this Client.

   Please note that if this director is being used by a Monitor, we highly
   recommend to set this directive to {\bf yes} to avoid serious security
   problems.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Name}{}{}{%
   The name of the Director  that may contact this Client. This name must be the
   same as the name specified on the Director resource  in the Director's
   configuration file. Note, the case (upper/lower) of the characters in
   the name are significant (i.e. S is not the same as s). This directive
   is required.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{Password}{}{}{%
   Specifies the password that must be  supplied for a Director to be authorized.
   This password  must be the same as the password specified in the  Client
   resource in the Director's configuration file.  This directive is required.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Allowed CN}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Authenticate}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS CA Certificate Dir}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS CA Certificate File}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Certificate}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Certificate Revocation List}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS DH File}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Enable}{}{}{%
   Bareos can be configured to encrypt all its network traffic. See chapter \nameref{TlsDirectives} to see how the Bareos Director (and the other components) have to be configured to use TLS.
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Key}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Require}{}{}{%
   }

.. raw:: latex

   \defDirective{Fd}{Director}{TLS Verify Peer}{}{}{%
   }

Thus multiple Directors may be authorized to use this Client’s services.
Each Director will have a different name, and normally a different
password as well.

The following is an example of a valid Director resource definition:

.. raw:: latex

   \footnotesize

::

    #
    # List Directors who are permitted to contact the File daemon
    #
    Director {
      Name = HeadMan
      Password = very_good                # password HeadMan must supply
    }
    Director {
      Name = Worker
      Password = not_as_good
      Monitor = Yes
    }

.. raw:: latex

   \normalsize

.. _MessagesResource3:

Messages Resource
-----------------

.. index:: General; Messages Resource 

.. index:: 
   triple: General; Resource; Messages

Please see the :ref:`Messages Resource MessagesChapter`
Chapter of this manual for the details of the Messages Resource.

There must be at least one Message resource in the Client configuration
file.

.. _SampleClientConfiguration:

Example Client Configuration File
---------------------------------

An example File Daemon configuration file might be the following:

.. raw:: latex

   \footnotesize

::

    #
    # Default  Bareos File Daemon Configuration file
    #
    #  For Bareos release 12.4.4 (12 June 2013)
    #
    # There is not much to change here except perhaps the
    # File daemon Name to
    #

    #
    # List Directors who are permitted to contact this File daemon
    #
    Director {
      Name = bareos-dir
      Password = "aEODFz89JgUbWpuG6hP4OTuAoMvfM1PaJwO+ShXGqXsP"
    }

    #
    # Restricted Director, used by tray-monitor to get the
    #   status of the file daemon
    #
    Director {
      Name = client1-mon
      Password = "8BoVwTju2TQlafdHFExRIJmUcHUMoIyIqPJjbvcSO61P"
      Monitor = yes
    }

    #
    # "Global" File daemon configuration specifications
    #
    FileDaemon {                          # this is me
      Name = client1-fd
      Maximum Concurrent Jobs = 20

      # remove comment in next line to load plugins from specified directory
      # Plugin Directory = /usr/lib64/bareos/plugins
    }

    # Send all messages except skipped files back to Director
    Messages {
      Name = Standard
      director = client1-dir = all, !skipped, !restored
    }

.. raw:: latex

   \normalsize
