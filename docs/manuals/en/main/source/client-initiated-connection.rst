.. _sec:ClientInitiatedConnection:

Client Initiated Connection
===========================

The :raw-latex:`\bareosDir `knows, when it is required to talk to a
client ( |bareosFd| ). Therefore, by defaults, the
:raw-latex:`\bareosDir `connects to the clients.

However, there are setups where this can cause problems, as this means
that:

-  The client must be reachable by its configured
   :raw-latex:`\linkResourceDirective{Dir}{Client}{Address}`. Address
   can be the DNS name or the IP address. (For completeness: there are
   potential workarounds by using the
   :ref:`setip bcommandSetIP` command.)

-  The :raw-latex:`\bareosDir `must be able to connect to the
   :raw-latex:`\bareosFd `over the network.

To circumvent these problems, since Bareos
16.2.2 it
is possible to let the :raw-latex:`\bareosFd `initiate the network
connection to the  |bareosDir| .

Which address the client connects to reach the
:raw-latex:`\bareosDir `is configured in the
:raw-latex:`\linkResourceDirective{Fd}{Director}{Address}` directive.

To additional allow this connection direction use:

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Connection From Client To Director}`
   = yes

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Heartbeat Interval}`
   = 60 ``#`` to keep the network connection established

-  :raw-latex:`\linkResourceDirective{Fd}{Director}{Connection From Client To Director}`
   = yes

To only allow Connection From the Client to the Director use:

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Connection From Director To Client}`
   = no

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Connection From Client To Director}`
   = yes

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Heartbeat Interval}`
   = 60 ``#`` to keep the network connection established

-  :raw-latex:`\linkResourceDirective{Fd}{Director}{Connection From Director To Client}`
   = no

-  :raw-latex:`\linkResourceDirective{Fd}{Director}{Connection From Client To Director}`
   = yes

Using Client Initiated Connections has disadvantages. Without Client
Initiated Connections the :raw-latex:`\bareosDir `only establishes a
network connection when this is required. With Client Initiated
Connections, the :raw-latex:`\bareosFd `connects to the
:raw-latex:`\bareosDir `and the :raw-latex:`\bareosDir `keeps these
connections open. The command :command:`status dir` will
show all waiting connections:

.. raw:: latex

   \begin{bconsole}{show waiting client connections}
   *<input>status dir</input>
   ...
   Client Initiated Connections (waiting for jobs):
   Connect time        Protocol            Authenticated       Name
   ====================================================================================================
   19-Apr-16 21:50     54                  1                   client1.example.com
   ...
   ====
   \end{bconsole}

When both connection directions are allowed, the
:raw-latex:`\bareosDir `

#. checks, if there is a waiting connection from this client.

#. tries to connect to the client (using the usual timeouts).

#. waits for a client connection to appear (using the same timeout as
   when trying to connect to a client).

If none of this worked, the job fails.

When a waiting connection is used for a job, the
:raw-latex:`\bareosFd `will detect this and creates an additional
connection. This is required, to keep the client responsive for
additional commands, like :command:`cancel `.

To get feedback in case the :raw-latex:`\bareosFd `fails to connect to
the  |bareosDir| , consider configuring
:raw-latex:`\bareosFd `to log in a local file. This can be archived by
adding the line

.. raw:: latex

   \configline{Append = "/var/log/bareos/bareos-fd.log" = all, !skipped, !restored}

to the default message resource
:raw-latex:`\resourcename{Fd}{Messages}{Standard}`:

.. raw:: latex

   \begin{bareosConfigResource}{bareos-fd}{messages}{Standard}
   Messages {
     Name = Standard
     Director = bareos-dir = all, !skipped, !restored
     Append = "/var/log/bareos/bareos-fd.log" = all, !skipped, !restored
   }
   \end{bareosConfigResource}
