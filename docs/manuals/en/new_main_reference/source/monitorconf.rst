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
:ref:`ConfigureChapter Configuration` chapter of this
manual.

The following Monitor Resource definition must be defined:

-  :ref:`MonitorResource Monitor` – to define the
   Monitor’s name used to connect to all the daemons and the password
   used to connect to the Directors. Note, you must not define more than
   one Monitor resource in the Monitor configuration file.

-  At least one :ref:`ClientResource1 Client`,
   :ref:`StorageResource1 Storage` or
   :ref:`DirectorResource2 Director` resource, to define
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
in the :ref:`DirectorChapter Director's configuration`
file, using the Console Name and Password defined in the Monitor
resource. To avoid security problems, you should configure this Console
resource to allow access to no other daemons, and permit the use of only
two commands: **status** and **.status** (see below for an example).

You may have multiple Director resource specifications in a single
Monitor configuration file.

.. _ClientResource1:

Client Resource
---------------


.. index:: 
   triple: General; Resource; Client
.. index:: General; Client Resource 

The Client resource defines the attributes of the Clients that are
monitored by this Monitor.

You must create a Director resource in the
:ref:`FiledConfChapter Client's configuration` file,
using the Director Name defined in the Monitor resource. To avoid
security problems, you should set the **Monitor** directive to **Yes**
in this Director resource.

You may have multiple Director resource specifications in a single
Monitor configuration file.

.. _StorageResource1:

Storage Resource
----------------


.. index:: 
   triple: General; Resource; Storage
.. index:: General; Storage Resource 

The Storage resource defines the attributes of the Storages that are
monitored by this Monitor.

You must create a Director resource in the
:ref:`StoredConfChapter Storage's configuration` file,
using the Director Name defined in the Monitor resource. To avoid
security problems, you should set the **Monitor** directive to **Yes**
in this Director resource.

You may have multiple Director resource specifications in a single
Monitor configuration file.

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
:ref:`SampleClientConfiguration`.

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
:ref:`ExampleStorageConfiguration`.

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
:ref:`SampleDirectorConfiguration`.
