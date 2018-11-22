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
:ref:`ConfigureChapter Configuration` chapter of this
manual. The following Client Resource definitions must be defined:

-  :ref:`ClientResourceClient Client` – to define what
   Clients are to be backed up.

-  :ref:`ClientResourceDirector Director` – to define the
   Director’s name and its access password.

-  :ref:`MessagesChapter Messages` – to define where
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

Please see the :ref:`MessagesChapter Messages Resource`
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
