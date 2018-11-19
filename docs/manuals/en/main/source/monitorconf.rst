.. _sec:MonitorConfig:

Monitor Configuration
=====================

.. index:: General; Monitor Configuration 

.. index:: 
   triple: General; Configuration; Monitor

The Monitor configuration file is a stripped down version of the
Director configuration file, mixed with a Console configuration file. It
simply contains the information necessary to contact Directors, Clients,
and Storage daemons you want to monitor.

For a general discussion of configuration file and resources including
the data types recognized by **Bareos**, please see the
:ref:`Configuration ConfigureChapter` chapter of this
manual.

The following Monitor Resource definition must be defined:

-  :ref:`Monitor MonitorResource` – to define the
   Monitor’s name used to connect to all the daemons and the password
   used to connect to the Directors. Note, you must not define more than
   one Monitor resource in the Monitor configuration file.

-  At least one :ref:`Client ClientResource1`,
   :ref:`Storage StorageResource1` or
   :ref:`Director DirectorResource2` resource, to define
   the daemons to monitor.

.. _MonitorResource:

Monitor Resource
----------------

.. index:: General; Monitor Resource 

.. index:: 
   triple: General; Resource; Monitor

The Monitor resource defines the attributes of the Monitor running on
the network. The parameters you define here must be configured as a
Director resource in Clients and Storages configuration files, and as a
Console resource in Directors configuration files.

.. raw:: latex

   \defDirective{Console}{Monitor}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{Dir Connect Timeout}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{FD Connect Timeout}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{Name}{}{}{%
   Specifies the Director name used to connect to Client and Storage, and the
   Console name used to connect to Director. This record is required.
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{Password}{}{}{%
   Where the password is needed for Directors to accept the Console
   connection. This password must be identical to the {\bf Password} specified
   in the {\bf Console} resource of the \ilink{Director's configuration}{DirectorChapter}
   file. This record is required if you wish to monitor Directors.
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{Refresh Interval}{}{}{%
   Specifies the time to wait  between status requests to each daemon. It can't
   be set to less than  1 second or more than 10 minutes.
   % TODO: what is format of the time?
   % TODO: should the digits in this  definition be spelled out? should
   % TODO: this say "time-period-specification" above??)
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{Require SSL}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Monitor}{SD Connect Timeout}{}{}{%
   }

.. _DirectorResource2:

Director Resource
-----------------

.. index:: General; Director Resource 

.. index:: 
   triple: General; Resource; Director

The Director resource defines the attributes of the Directors that are
monitored by this Monitor.

As you are not permitted to define a Password in this resource, to avoid
obtaining full Director privileges, you must create a Console resource
in the :ref:`Director's configuration DirectorChapter`
file, using the Console Name and Password defined in the Monitor
resource. To avoid security problems, you should configure this Console
resource to allow access to no other daemons, and permit the use of only
two commands: **status** and **.status** (see below for an example).

You may have multiple Director resource specifications in a single
Monitor configuration file.

.. raw:: latex

   \defDirective{Console}{Director}{Address}{}{}{%
   Where the address is a host name,  a fully qualified domain name, or a network
   address used to connect  to the Director. This record is required.
   }

.. raw:: latex

   \defDirective{Console}{Director}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{Dir Port}{}{}{%
   Specifies the port to use to connect  to the Director.
   This port must be
   identical to the  {\bf DIRport} specified in the {\bf Director} resource of the
   \nameref{DirectorChapter} file.
   }

.. raw:: latex

   \defDirective{Console}{Director}{Enable SSL}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{Name}{}{}{%
   The Director name used to identify  the Director in the list of monitored
   daemons. It is not required  to be the same as the one defined in the Director's
   configuration file.  This record is required.
   }

.. _ClientResource1:

Client Resource
---------------


.. index:: 
   triple: General; Resource; Client
.. index:: General; Client Resource 

The Client resource defines the attributes of the Clients that are
monitored by this Monitor.

You must create a Director resource in the
:ref:`Client's configuration FiledConfChapter` file,
using the Director Name defined in the Monitor resource. To avoid
security problems, you should set the **Monitor** directive to **Yes**
in this Director resource.

You may have multiple Director resource specifications in a single
Monitor configuration file.

.. raw:: latex

   \defDirective{Console}{Client}{Address}{}{}{%
   Where the address is a host  name, a fully qualified domain name, or a network
   address in  dotted quad notation for a Bareos File daemon.  This record is
   required.
   }

.. raw:: latex

   \defDirective{Console}{Client}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Client}{Enable SSL}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Client}{FD Port}{}{}{%
   Where the port is a port  number at which the Bareos File daemon can be
   contacted.
   }

.. raw:: latex

   \defDirective{Console}{Client}{Name}{}{}{%
   The Client name used to identify  the Director in the list of monitored
   daemons. It is not required  to be the same as the one defined in the Client's
   configuration file. This record is required.
   }

.. raw:: latex

   \defDirective{Console}{Client}{Password}{}{}{%
   This is the password to be  used when establishing a connection with the File
   services, so  the Client configuration file on the machine to be backed up
   must  have the same password defined for this Director. This record is
   required.
   }

.. _StorageResource1:

Storage Resource
----------------


.. index:: 
   triple: General; Resource; Storage
.. index:: General; Storage Resource 

The Storage resource defines the attributes of the Storages that are
monitored by this Monitor.

You must create a Director resource in the
:ref:`Storage's configuration StoredConfChapter` file,
using the Director Name defined in the Monitor resource. To avoid
security problems, you should set the **Monitor** directive to **Yes**
in this Director resource.

You may have multiple Director resource specifications in a single
Monitor configuration file.

.. raw:: latex

   \defDirective{Console}{Storage}{Address}{}{}{%
   Where the address is a host name, a fully qualified domain name, or a network
   address in  dotted quad notation for a Bareos Storage daemon.  This record is
   required.
   }

.. raw:: latex

   \defDirective{Console}{Storage}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Storage}{Enable SSL}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Storage}{Name}{}{}{%
   The Storage name used to identify  the Director in the list of monitored
   daemons. It is not required  to be the same as the one defined in the Storage's
   configuration file. This record is required.
   }

.. raw:: latex

   \defDirective{Console}{Storage}{Password}{}{}{%
   This is the password to be used  when establishing a connection with the
   Storage services. This  same password also must appear in the Director
   resource of the Storage  daemon's configuration file. This record is required.
   }

.. raw:: latex

   \defDirective{Console}{Storage}{SD Address}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Storage}{SD Password}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Storage}{SD Port}{}{}{%
   Where port is the port to use to  contact the storage daemon for information
   and to start jobs. This same port number must appear in the Storage resource
   of the  Storage daemon's configuration file.
   }

Tray Monitor
------------

Tray Monitor Security
~~~~~~~~~~~~~~~~~~~~~

.. index:: General; Tray Monitor Security 

.. index:: 
   triple: General; Security; Tray Monitor

There is no security problem in relaxing the permissions on
tray-monitor.conf as long as FD, SD and DIR are configured properly, so
the passwords contained in this file only gives access to the status of
the daemons. It could be a security problem if you consider the status
information as potentially dangerous (most people consider this as not
being dangerous).

| Concerning Director’s configuration:
| In tray-monitor.conf, the password in the Monitor resource must point
  to a restricted console in bareos-dir.conf (see the documentation).
  So, if you use this password with bconsole, you’ll only have access to
  the status of the director (commands status and .status). It could be
  a security problem if there is a bug in the ACL code of the director.

| Concerning File and Storage Daemons’ configuration:
| In tray-monitor.conf, the Name in the Monitor resource must point to a
  Director resource in bareos-fd/sd.conf, with the Monitor directive set
  to **Yes** (see the documentation). It could be a security problem if
  there is a bug in the code which check if a command is valid for a
  Monitor (this is very unlikely as the code is pretty simple).

Example Tray Monitor configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Tray Monitor; Configuration

.. index:: 
   triple: General; Configuration; Tray Monitor

An example Tray Monitor configuration file might be the following:

.. raw:: latex

   \begin{bconfig}{Example tray-monitor.conf}
   #
   # Bareos Tray Monitor Configuration File
   #
   Monitor {
     Name = rufus-mon        # password for Directors
     Password = "GN0uRo7PTUmlMbqrJ2Gr1p0fk0HQJTxwnFyE4WSST3MWZseR"
     RefreshInterval = 10 seconds
   }

   Client {
     Name = rufus-fd
     Address = rufus
     FDPort = 9102           # password for FileDaemon
     Password = "FYpq4yyI1y562EMS35bA0J0QC0M2L3t5cZObxT3XQxgxppTn"
   }
   Storage {
     Name = rufus-sd
     Address = rufus
     SDPort = 9103           # password for StorageDaemon
     Password = "9usxgc307dMbe7jbD16v0PXlhD64UVasIDD0DH2WAujcDsc6"
   }
   Director {
     Name = rufus-dir
     DIRport = 9101
     address = rufus
   }
   \end{bconfig}

Example File daemon’s Director record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: latex

   \begin{bconfig}{Example Monitor resource}
   #
   # Restricted Director, used by tray-monitor to get the
   #   status of the file daemon
   #
   Director {
     Name = rufus-mon
     Password = "FYpq4yyI1y562EMS35bA0J0QC0M2L3t5cZObxT3XQxgxppTn"
     Monitor = yes
   }
   \end{bconfig}

A full example can be found at
.. _SampleClientConfiguration: .

Example Storage daemon’s Director record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: latex

   \begin{bconfig}{Example Monitor resource}
   #
   # Restricted Director, used by tray-monitor to get the
   #   status of the storage daemon
   #
   Director {
     Name = rufus-mon
     Password = "9usxgc307dMbe7jbD16v0PXlhD64UVasIDD0DH2WAujcDsc6"
     Monitor = yes
   }
   \end{bconfig}

A full example can be found at
.. _ExampleStorageConfiguration: .

Example Director’s Console record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: latex

   \begin{bconfig}{Example Monitor resource}
   #
   # Restricted console used by tray-monitor to get the status of the director
   #
   Console {
     Name = Monitor
     Password = "GN0uRo7PTUmlMbqrJ2Gr1p0fk0HQJTxwnFyE4WSST3MWZseR"
     CommandACL = status, .status
   }
   \end{bconfig}

A full example can be found at
.. _SampleDirectorConfiguration: .
