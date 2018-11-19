.. _PassiveClient:

Passive Clients
===============

The normal way of initializing the data channel (the channel where the
backup data itself is transported) is done by the
:raw-latex:`\bareosFd `(client) that connects to the
 |bareosSd| .

In many setups, this can cause problems, as this means that:

-  The client must be able to resolve the name of the
   :raw-latex:`\bareosSd `(often not true, you have to do tricks with
   the hosts file)

-  The client must be allowed to create a new connection.

-  The client must be able to connect to the :raw-latex:`\bareosSd `over
   the network (often difficult over NAT or Firewall)

By using Passive Client, the initialization of the datachannel is
reversed, so that the storage daemon connects to the
 |bareosFd| . This solves almost every problem created by
firewalls, NAT-gateways and resolving issues, as

-  The :raw-latex:`\bareosSd `initiates the connection, and thus can
   pass through the same or similar firewall rules that the director
   already has to access the  |bareosFd| .

-  The client never initiates any connection, thus can be completely
   firewalled.

-  The client never needs any name resolution and is totally independent
   from any resolving issues.

|image|

Usage
-----

To use this new feature, just configure
:raw-latex:`\linkResourceDirective{Dir}{Client}{Passive}`=yes in the
client definition of the  |bareosDir| :

.. raw:: latex

   \begin{bconfig}{Enable passive mode in bareos-dir.conf}
   Client {
      Name = client1-fd
      Password = "secretpassword"
      <input>Passive = yes</input>
      [...]
   }
   \end{bconfig}

Also, prior to bareos version 15, you need to set
:raw-latex:`\linkResourceDirective{Fd}{Client}{Compatible}`=no in the
*bareos-fd.conf* configuration file. Since Bareos
Version 15, the compatible option is set to no per default and does not
need to be specified anymore.

.. raw:: latex

   \begin{bconfig}{Disable compatible mode for the \bareosFd in bareos-fd.conf} 
   Director {
     Name = bareos-dir
     Password = "secretpassword"
   }

   Client {
      Name = client1-fd
      [...]
      <input>Compatible = no</input>
   }
   \end{bconfig}

.. |image| image:: \idir passive-client-communication
   :width: 60.0%
