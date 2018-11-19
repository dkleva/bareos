.. _ConsoleConfChapter:

Console Configuration
=====================


.. index:: 
   triple: General; Configuration; Console
.. index:: General; Console Configuration 

The Console configuration file is the simplest of all the configuration
files, and in general, you should not need to change it except for the
password. It simply contains the information necessary to contact the
Director or Directors.

For a general discussion of the syntax of configuration files and their
resources including the data types recognized by **Bareos**, please see
the :ref:`Configuration ConfigureChapter` chapter of this
manual.

The following Console Resource definition must be defined:

.. _ConsoleResourceDirector:

Director Resource
-----------------

.. index:: General; Director Resource 

.. index:: 
   triple: General; Resource; Director

The Director resource defines the attributes of the Director running on
the network. You may have multiple Director resource specifications in a
single Console configuration file. If you have more than one, you will
be prompted to choose one when you start the **Console** program.

.. raw:: latex

   \defDirective{Console}{Director}{Address}{}{}{%
   Where the address is a host name,  a fully qualified domain name, or a network
   address used to connect  to the Director.
   }

.. raw:: latex

   \defDirective{Console}{Director}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{Dir Port}{}{}{%
   This port must be identical to the
   \linkResourceDirective{Dir}{Director}{Dir Port} specified in the \nameref{DirectorChapter} file.
   }

.. raw:: latex

   \defDirective{Console}{Director}{Heartbeat Interval}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{Name}{}{}{%
   The director name used to select among different Directors, otherwise, this
   name is not used.
   }

.. raw:: latex

   \defDirective{Console}{Director}{Password}{}{}{%
   This password is used to authenticate when connecting to the \bareosDir as default console.
   It must correspond to \linkResourceDirective{Dir}{Director}{Password}.
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Authenticate}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS CA Certificate Dir}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS CA Certificate File}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Certificate}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Certificate Revocation List}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Enable}{}{}{%
   Bareos can be configured to encrypt all its network traffic. See chapter \nameref{TlsDirectives} to see how the Bareos Director (and the other components) have to be configured to use TLS.
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Key}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Require}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Director}{TLS Verify Peer}{}{}{%
   }

An actual example might be:

.. raw:: latex

   \footnotesize

::

    Director {
      Name = HeadMan
      address = rufus.cats.com
      password = xyz1erploit
    }

.. raw:: latex

   \normalsize

.. raw:: latex

   \hide{
   \section{ConsoleFont Resource}
   \index[general]{Resource!ConsoleFont}
   \index[general]{ConsoleFont Resource}

   The ConsoleFont resource is available only in the GNOME version of the
   console. It permits you to define the font that you want used to display in
   the main listing window.

   \begin{description}

   \item [ConsoleFont]
   \index[console]{ConsoleFont}
   Start of the ConsoleFont directives.

   \item [Name = {\textless}name{\textgreater}] \hfill \\
   \index[console]{Name}
   The name of the font.

   \item [Font = {\textless}Pango Font Name{\textgreater}] \hfill \\
   \index[console]{Font}
   The string value given here defines the desired font. It  is specified in the
   Pango format. For example, the default specification is:

   \footnotesize
   \begin{verbatim}
   Font = "LucidaTypewriter 9"
   \end{verbatim}
   \normalsize

   \end{description}

   Thanks to Phil Stracchino for providing the code for this feature.

   An different example might be:

   \footnotesize
   \begin{verbatim}
   ConsoleFont {
     Name = Default
     Font = "Monospace 10"
   }
   \end{verbatim}
   \normalsize
   }

.. _ConsoleResourceConsole:

Console Resource
----------------

.. index:: General; Console Resource 

.. index:: 
   triple: General; Resource; Console

There are three different kinds of consoles, which the administrator or
user can use to interact with the Director. These three kinds of
consoles comprise three different security levels.

-  The first console type is an **admin** or
   **anonymous}` or :raw-latex:`\name{default** console,
   which has full privileges. There is no console resource necessary for
   this type since the password is specified in the Director resource.
   Typically you would use this console only for administrators.

-  The second type of console is a "named" or "restricted" console
   defined within a Console resource in both the Director’s
   configuration file and in the Console’s configuration file. Both the
   names and the passwords in these two entries must match much as is
   the case for Client programs.

   This second type of console begins with absolutely no privileges
   except those explicitly specified in the Director’s Console resource.
   Note, the definition of what these restricted consoles can do is
   determined by the Director’s conf file.

   Thus you may define within the Director’s conf file multiple Consoles
   with different names and passwords, sort of like multiple users, each
   with different privileges. As a default, these consoles can do
   absolutely nothing – no commands what so ever. You give them
   privileges or rather access to commands and resources by specifying
   access control lists in the Director’s Console resource. This gives
   the administrator fine grained control over what particular consoles
   (or users) can do.

-  The third type of console is similar to the above mentioned
   restricted console in that it requires a Console resource definition
   in both the Director and the Console. In addition, if the console
   name, provided on the **Name =** directive, is the same as a Client
   name, the user of that console is permitted to use the **SetIP**
   command to change the Address directive in the Director’s client
   resource to the IP address of the Console. This permits portables or
   other machines using DHCP (non-fixed IP addresses) to "notify" the
   Director of their current IP address.

The Console resource is optional and need not be specified. However, if
it is specified, you can use ACLs (Access Control Lists) in the
Director’s configuration file to restrict the particular console (or
user) to see only information pertaining to his jobs or client machine.

You may specify as many Console resources in the console’s conf file. If
you do so, generally the first Console resource will be used. However,
if you have multiple Director resources (i.e. you want to connect to
different directors), you can bind one of your Console resources to a
particular Director resource, and thus when you choose a particular
Director, the appropriate Console configuration resource will be used.
See the "Director" directive in the Console resource described below for
more information.

Note, the Console resource is optional, but can be useful for restricted
consoles as noted above.

.. raw:: latex

   \defDirective{Console}{Console}{Description}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{Director}{}{}{%
   If this directive is specified, this Console resource will be
   used by bconsole when that particular director is selected
   when first starting bconsole.  I.e. it binds a particular console
   resource with its name and password to a particular director.
   }

.. raw:: latex

   \defDirective{Console}{Console}{Heartbeat Interval}{}{}{%
   This directive is optional and if specified will cause the Console to
   set a keepalive interval (heartbeat) in seconds on each of the sockets
   to communicate with the Director.  It is implemented only on systems
   (Linux, ...) that provide the {\bf setsockopt} TCP\_KEEPIDLE function.
   If the value is set to 0 (zero), no change is made to the socket.
   }

.. raw:: latex

   \defDirective{Console}{Console}{History File}{}{}{%
   If this directive is specified and the console is compiled with readline support,
   it will use the given filename as history file.
   If not specified, the history file will be named \file{~/.bconsole_history}
   }

.. raw:: latex

   \defDirective{Console}{Console}{History Length}{}{}{%
   If this directive is specified the history file will be truncated after \configdirective{HistoryLength} entries.
   }

.. raw:: latex

   \defDirective{Console}{Console}{Name}{}{}{%
   The Console name used to allow a restricted console to change
   its IP address using the SetIP command. The SetIP command must
   also be defined in the Director's conf CommandACL list.
   }

.. raw:: latex

   \defDirective{Console}{Console}{Password}{}{}{%
   If this password is supplied, then the password specified in the
   Director resource of you Console conf will be ignored.  See below
   for more details.
   }

.. raw:: latex

   \defDirective{Console}{Console}{Rc File}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Authenticate}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS CA Certificate Dir}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS CA Certificate File}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Certificate}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Certificate Revocation List}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Enable}{}{}{%
   Bareos can be configured to encrypt all its network traffic. See chapter \nameref{TlsDirectives} to see how the Bareos Director (and the other components) have to be configured to use TLS.
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Key}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Require}{}{}{%
   }

.. raw:: latex

   \defDirective{Console}{Console}{TLS Verify Peer}{}{}{%
   }

Example Console Configuration File
----------------------------------


.. index:: 
   triple: General; Configuration; bconsole

A Console configuration file might look like this:

.. raw:: latex

   \begin{bconfig}{bconsole configuration}
   Director {
     Name = "bareos.example.com-dir"
     address = "bareos.example.com"
     Password = "PASSWORD"
   }
   \end{bconfig}

With this configuration, the console program (e.g.
:command:`bconsole`) will try to connect to a
:raw-latex:`\bareosDir `named **bareos.example.com-dir**
at the network address **bareos.example.com** and
authenticate to the admin console using the password
**PASSWORD**.

.. _sec:ConsoleAccessExample:

Using Named Consoles
~~~~~~~~~~~~~~~~~~~~

The following configuration files were supplied by Phil Stracchino.

To use named consoles from :command:`bconsole`, use a
*bconsole.conf* configuration file like this:

.. raw:: latex

   \begin{bconfig}{bconsole: restricted-user}
   Director {
      Name = bareos-dir
      Address = myserver
      Password = "XXXXXXXXXXX"
   }

   Console {
      Name = restricted-user
      Password = "RUPASSWORD"
   }
   \end{bconfig}

Where the Password in the Director section is deliberately incorrect and
the Console resource is given a name, in this case
**restricted-user**. Then in the Director
configuration (not directly accessible by the user), we define:

.. raw:: latex

   \begin{bareosConfigResource}{bareos-dir}{console}{restricted-user}
   Console {
     Name = restricted-user
     Password = "RUPASSWORD"
     JobACL = "Restricted Client Save"
     ClientACL = restricted-client
     StorageACL = main-storage
     ScheduleACL = *all*
     PoolACL = *all*
     FileSetACL = "Restricted Client's FileSet"
     CatalogACL = MyCatalog
     CommandACL = run
   }
   \end{bareosConfigResource}

The user login into the Director from his Console will get logged in as
:raw-latex:`\resourcename{Dir}{Console}{restricted-user}` and he will
only be able to see or access a Job with the name
:raw-latex:`\resourcename*{Dir}{Job}{Restricted Client Save}`, a Client
with the name
:raw-latex:`\resourcename*{Dir}{Client}{restricted-client}`, a storage
device :raw-latex:`\resourcename*{Dir}{Storage}{main-storage}`, any
Schedule or Pool, a FileSet named
:raw-latex:`\resourcename*{Dir}{FileSet}{Restricted Client's FileSet}`,
a Catalog named :raw-latex:`\resourcename*{Dir}{Catalog}{MyCatalog}` and
the only command he can use in the Console is the
:command:`run ` command. In other words, this user is
rather limited in what he can see and do with Bareos. For details how to
configure ACLs, see the :raw-latex:`\dt{Acl}` data type description.

The following is an example of a *bconsole.conf* file
that can access several Directors and has different Consoles depending
on the Director:

.. raw:: latex

   \begin{bconfig}{bconsole: multiple consoles}
   Director {
      Name = bareos-dir
      Address = myserver
      Password = "XXXXXXXXXXX"    # no, really.  this is not obfuscation.
   }

   Director {
      Name = SecondDirector
      Address = secondserver
      Password = "XXXXXXXXXXX"    # no, really.  this is not obfuscation.
   }

   Console {
      Name = restricted-user
      Password = "RUPASSWORD"
      Director = MyDirector
   }

   Console {
      Name = restricted-user2
      Password = "OTHERPASSWORD"
      Director = SecondDirector
   }
   \end{bconfig}

The second Director referenced at
:raw-latex:`\resourcename{Dir}{Director}{secondserver}` might look like
the following:

.. raw:: latex

   \begin{bareosConfigResource}{bareos-dir}{console}{restricted-user2}
   Console {
     Name = restricted-user2
     Password = "OTHERPASSWORD"
     JobACL = "Restricted Client Save"
     ClientACL = restricted-client
     StorageACL = second-storage
     ScheduleACL = *all*
     PoolACL = *all*
     FileSetACL = "Restricted Client's FileSet"
     CatalogACL = RestrictedCatalog
     CommandACL = run, restore
     WhereACL = "/"
   }
   \end{bareosConfigResource}
