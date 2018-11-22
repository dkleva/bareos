The Bareos project provides and supports packages that have been
released at http://download.bareos.org/bareos/release/

However, the following tabular gives an overview, what components are
expected on which platforms to run:

+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| **Operating Systems**                                                                          | **Version**        | **Client Daemon**                                                               | **Director Daemon**                                                             | **Storage Daemon**                                                              |
+================================================================================================+====================+=================================================================================+=================================================================================+=================================================================================+
| :raw-latex:`\multicolumn{5}{c}{\textbf{Linux}}` 
.. index:: 
   triple: General; Platform; Linux   |                    |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Arch Linux 
.. index:: 
   triple: General; Platform; Arch Linux}`                                   |                    | https://aur.archlinux.org/pkgbase/bareos/               | :raw-latex:`\elink{X}{https://aur.archlinux.org/pkgbase/bareos/               |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| CentOS                                                                                         | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Debian                                                                                         | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Fedora                                                                                         | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Gentoo 
.. index:: 
   triple: General; Platform; Gentoo}`                                           |                    | https://packages.gentoo.org/package/app-backup/bareos   | :raw-latex:`\elink{X}{https://packages.gentoo.org/package/app-backup/bareos   |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| openSUSE                                                                                       | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| RHEL                                                                                           | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| SLES                                                                                           | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Ubuntu                                                                                         | current            | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :ref:`Univention Corporate Linux sec:UniventionCorporateServer`                 | App Center         | v12.4                                                                           | v12.4                                                                           | v12.4                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :raw-latex:`\multicolumn{5}{c}{\textbf{MS Windows}}`                                           |                    |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :ref:`MS Windows sec:windows` 32bit                                             | 10/8/7             | v12.4                                                                           | v15.2                                                                           | v15.2                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
|                                                                                                | 2008/Vista         |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
|                                                                                                | 2003/XP            | v12.4–v14.2                                                                     |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :ref:`MS Windows sec:windows` 64bit                                             | 10/8/2012/7        | v12.4                                                                           | v15.2                                                                           | v15.2                                                                           |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
|                                                                                                | 2008/Vista         |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :raw-latex:`\multicolumn{5}{c}{\textbf{Mac OS}}`                                               |                    |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :ref:`Mac OS X/Darwin sec:macosx`                                               |                    | v14.2                                                                           |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :raw-latex:`\multicolumn{5}{c}{\textbf{BSD}}`                                                  |                    |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| FreeBSD 
.. index:: 
   triple: General; Platform; FreeBSD}`                                         | :math:`\geq` 5.0   | http://www.freshports.org/sysutils/bareos-server/       | :raw-latex:`\elink{X}{http://www.freshports.org/sysutils/bareos-server/       |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| OpenBSD                                                                                        |                    | X                                                                               |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| NetBSD                                                                                         |                    | X                                                                               |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| :raw-latex:`\multicolumn{5}{c}{\textbf{Unix}}`                                                 |                    |                                                                                 |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| AIX 
.. index:: 
   triple: General; Platform; AIX                                                 | :math:`\geq` 4.3   | com-13.2                                                                        | :math:`\star`                                                                   | :math:`\star`                                                                   |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| HP-UX 
.. index:: 
   triple: General; Platform; HP-UX                                             |                    | com-13.2                                                                        |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Irix                                                                                           |                    | :math:`\star`                                                                   |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Solaris 
.. index:: 
   triple: General; Platform; Solaris                                         | :math:`\geq` 8     | com-12.4                                                                        | com-12.4                                                                        | com-12.4                                                                        |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| True64                                                                                         |                    | :math:`\star`                                                                   |                                                                                 |                                                                                 |
+------------------------------------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

+---------------------+---------------------------------------------------------------------------------------------------------------------------------+
| **vVV.V**           | starting with Bareos version VV.V, this platform is official supported by the Bareos.org project                                |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+
| **com-VV.V**        | starting with Bareos version VV.V, this platform is supported. However, pre-build packages are only available from Bareos.com   |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+
| **nightly**         | provided by Bareos nightly build. Bug reports are welcome, however it is not official supported                                 |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+
| **X**               | known to work                                                                                                                   |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+
| **:math:`\star`**   | has been reported to work by the community                                                                                      |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+

Packages for the different Linux platforms
------------------------------------------

The following tables summarize what packages are available for the
different Linux platforms.

This information is generated based on
http://download.bareos.com/bareos/release/. In most cases this is
identical to the packages provided by
http://download.bareos.org/bareos/release/. Only if a package have been
added later in a maintenance release, these information may differ.

Distributions that are no longer relevant are left out. However, you
might still find the packages on our download servers.

Bareos tries to provide all packages for all current platforms. For
extra packages, it depends if the distribution contains the required
dependencies.

For general information about the packages, see
:ref:`sec:BareosPackages`.

Packages names not containing the word **bareos** are
required packages where we decided to include them ourselves.

:raw-latex:`\small`

Univention Corporate Server
---------------------------


.. index:: 
   triple: General; Platform; Univention Corporate Server The
Bareos version for the Univention App Center integraties into the
Univention Enterprise Linux environment, making it easy to backup all
the systems managed by the central Univention Corporate Server.

Preamble
~~~~~~~~

The
http://www.univention.de/
is an enterprise Linux distribution based on Debian. It consists of an
integrated management system for the centralised administration of
servers, computer workplaces, users and their rights as well as a wide
range of server applications. It also includes an Unvention App Center
for the easy installation and management of extensions and appliances.

Bareos is part of the
https://www.univention.de/produkte/univention-app-center/app-katalog/bareos/
and therefore an Univention environment can easily be extended to
provide backup functionality for the Univention servers as well as for
the connected client systems. Using the Univention Management Console
(UMC), you can also create backup jobs for client computers (Windows or
Linux systems), without the need of editing configuration files.

The Bareos Univention App is shipped with a default configuration for
the director daemon and the storage daemon.


.. warning:: 
  You need to review some Univention configuration registry (UCR) variables. Most likely, you will want to set the location where the backups are stored. Otherwise, you may quickly run out of disk space on your backup server!

You will find further information under
:ref:`sec:UniventionBackupStorage`.

Quick Start
~~~~~~~~~~~

-  Determine the space requirements and where to store your backup data

-  Set the **bareos/*** UCR variables according to
   your needs, see :ref:`sec:UCR`

-  Restart :command:`bareos-dir`,
   :command:`bareos-sd}` and :raw-latex:`\command{bareos-fd`
   (or simply reboot the server)

-  Install the Bareos file daemon on clients and copy Director
   configuration resource file from

   -  */etc/bareos/bareos-dir-export/client/<clientname>-fd/bareos-fd.d/director/*.conf*

   -  (or
      */etc/bareos/autogenerated/client-configs/<hostname>.conf*,
      if Bareos :math:`<` 16.2.0)

   For details, see :ref:`sec:UniventionAddClient`.

-  Enable backup jobs for clients in the Univention Management Console

UCR variables
~~~~~~~~~~~~~

**bareos/filestorage**
    : /var/lib/bareos/storage (default)

    -  Location where to store the backup files. Make sure, it offers
       enough disk space for a configured backup volumes.

**bareos/max_full_volume_bytes**
    : 20 (default)

    -  Maximum size (in GB) of a volume for the **Full**
       backup pool

**bareos/max_full_volumes**
    : 1 (default)

    -  Maximum number of volumes for the **Full** backup
       pool

**bareos/max_diff_volume_bytes**
    : 10 (default)

    -  Maximum size (in GB) of a volume for the
       **Differential** backup pool

**bareos/max_diff_volumes**
    : 1 (default)

    -  Maximum number of volumes for the
       **Differential** backup pool

**bareos/max_incr_volume_bytes**
    : 1 (default)

    -  Maximum size (in GB) of a volume for the
       **Incremental** backup pool

**bareos/max_incr_volumes**
    : 1 (default)

    -  Maximum number of volumes for the **Incremental**
       backup pool

**bareos/backup_myself**
    : no (default)

    no
        don’t backup the server itself

    yes
        backup the server itself

**bareos/webui/console/user1/username**
    : Administrator (default)

    -  User name to login at the bareos-webui

**bareos/webui/console/user1/password**
    : (no default value)

    -  Password to login at the bareos-webui

UCR variables can be set via the Univention Configuration Registry Web
interface

|image|

or using the :command:`ucr` command line tool:

.. raw:: latex

   \begin{commands}{Enable backup of the server itself}
   root@ucs:~# <input>ucr set bareos/backup_myself=yes</input>
   Setting bareos/backup_myself
   File: /etc/bareos/bareos-dir.conf
   [ ok ] Reloading Bareos Director: bareos-dir.
   \end{commands}


.. warning:: 
  univention-bareos $<$ 15.2 did require a manual reload/restart of the bareos-dir service:

.. raw:: latex

   \begin{commands}{let bareos-dir reload its configuration}
   root@ucs:~# <input>service bareos-dir reload</input>
   [ ok ] Reloading Bareos Director: bareos-dir.
   \end{commands}

Setup
~~~~~

After installation of the Bareos app, Bareos is ready for operation. A
default configuration is created automatically.

Bareos consists of three daemons called :command:`director`
(or :command:`bareos-dir`),
:command:`storage-daemon` (or
:command:`bareos-sd}`) and :raw-latex:`\command{filedaemon`
(or :command:`bareos-fd`). All three daemons are started
right after the installation by the Univention App Center.

If you want to enable automatic backups of the server, you need to set
the Univention configuration registry (UCR) variable
**bareos/backup_myself** to
**yes** and reload the director daemon.

Administration
~~~~~~~~~~~~~~

For general tasks the :ref:`bareos-webui sec:webui` can
be used. Additional, there is the :command:`bconsole`
command line tool:

.. raw:: latex

   \begin{commands}{Starting the bconsole}
   root@ucs:~# <input>bconsole</input>
   Connecting to Director ucs:9101
   1000 OK: ucs-dir Version: 15.2.2 (15 November 2015)
   Enter a period to cancel a command.
   *
   \end{commands}

For general information, see the
:ref:`Bconsole Tuturial sec:TuturialBconsole`.

Backup Schedule
~~~~~~~~~~~~~~~

As a result of the default configuration located at the
:command:`bareos-dir`, the backup schedule will look as
follows:

Full Backups
    -  are written into the **Full** pool

    -  on the first saturday at 21:00 o’clock

    -  and kept for 365 days

Differential Backups
    -  are written into the **Differential** pool

    -  on every 2nd to 5th saturday at 21:00 o’clock

    -  and kept for 90 days

Incremental Backups
    -  are written into the **Incremental** pool

    -  on every day from monday to friday at 21:00 o’clock

    -  and kept for 30 days

That means full backups will be written every first saturday at 21:00
o’clock, differential backups every 2nd to 5th saturday at 21:00 o’clock
and incremental backups from monday to friday at 21:00 o’clock. So you
have got one full backup every month, four weekly differential and 20
daily incremental backups per month.

This schedule is active for the Univention server backup of itself and
all other clients, which are backed up through the
:command:`bareos-dir` on the Univention server.

There is also a special backup task, which is the Bareos backups itself
for a possible disaster recovery. This backup has got its own backup
cycle which starts after the main backups. The backup consists of a
database backup for the metadata of the Bareos backup server and a
backup of the Bareos configuration files under
*/etc/bareos/*.

Backup data management
~~~~~~~~~~~~~~~~~~~~~~

Data from the backup jobs is written to volumes, which are organized in
pools (see chapter :ref:`DirectorResourcePool`).

The default configuration uses three different pools, called
**Full}`, :raw-latex:`\pool{Differential** and
**Incremental**, which are used for full backups,
differential and incremental backups, respectively.

If you change the UCR variables, the configuration files will be
rewritten automatically. After each change you will need to reload the
director daemon.

.. raw:: latex

   \begin{commands}{Example for changing the Full pool size to $10 \ast 20$ GB}
   root@ucs:~# <input>ucr set bareos/max_full_volumes=10</input>
   Setting bareos/max_full_volumes
   File: /etc/bareos/bareos-dir.conf
   [ ok ] Reloading Bareos Director: bareos-dir.
   root@ucs:~# <input>ucr set bareos/max_full_volume_bytes=20</input>
   Setting bareos/max_full_volume_bytes
   File: /etc/bareos/bareos-dir.conf
   [ ok ] Reloading Bareos Director: bareos-dir.
   \end{commands}


.. warning:: 
  This only affects new volumes. Existing volumes will not change there size.

Backup Storage
~~~~~~~~~~~~~~


.. warning:: 
  Using the default configuration, Bareos will store backups on your local disk. You may want to store the data to another location to avoid using up all of your disk space.

The location for backups is
:raw-latex:`\path`\|/var/lib/bareos/storage\| in the default
configuration.

For example, to use a NAS device for storing backups, you can mount your
NAS volume via NFS on :raw-latex:`\path`\|/var/lib/bareos/storage\|.
Alternatively, you can mount the NAS volume to another directory of your
own choice, and change the UCR variable
**bareos/filestorage** to the corresponding path.
The directory needs to be writable by user **bareos**.

.. raw:: latex

   \begin{commands}{Example for changing the storage path}
   root@ucs:/etc/bareos# <input>ucr set bareos/filestorage=/path/to/your/storage</input>
   Setting bareos/filestorage
   File: /etc/bareos/bareos-sd.conf
   \end{commands}


.. warning:: 
  You need to restart the Bareos storage daemon after having changed the storage path:

.. raw:: latex

   \begin{commands}{}
   root@ucs:/# <input>service bareos-sd restart</input>
   \end{commands}

Bareos Webui Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

After installation you just need to setup your login credentials via UCR
variables. Therefore, set the Univention configuration registry (UCR)
variable **bareos/webui/console/user1/username**
and **bareos/webui/consoles/user1/password**
according to your needs. The director configuration is automatically
reloaded if one of those two variables changes.

Alternatively you can also set those UCR variables via commandline.

.. raw:: latex

   \begin{commands}{Example for changing webui login credentials}
   root@ucs:~# <input>ucr set bareos/webui/console/user1/username="bareos"</input>
   Setting bareos/webui/console/user1/username
   File: /etc/bareos/bareos-dir.conf
   [ ok ] Reloading Bareos Director: bareos-dir.
   root@ucs:~# <input>ucr set bareos/webui/console/user1/password="secret"</input>
   Setting bareos/webui/console/user1/password
   File: /etc/bareos/bareos-dir.conf
   [ ok ] Reloading Bareos Director: bareos-dir.
   \end{commands}

When your login credentials are set, you can login into Bareos Webui by
following the entry in your Administration UCS Overview or directly via
`https://<UCS\_SERVER>/bareos-webui/ <https://<UCS_SERVER>/bareos-webui/>`__.

|image|

Add a client to the backup
~~~~~~~~~~~~~~~~~~~~~~~~~~

Overview
^^^^^^^^

-  Install the Bareos client software on the target system, see
   :ref:`Adding a Bareos Client SecondClient`

-  Use the Univention Management Console to add the client to the
   backup, see the screenshot below

-  Copy the filedaemon resource configuration file from the Univention
   server to the target system

Bareos :math:`>=` 16.2.4
^^^^^^^^^^^^^^^^^^^^^^^^

Server-side
'''''''''''

The Univention Bareos application comes with an automatism for the
client and job configuration. If you want to add a client to the Bareos
director configuration, you need use the Univention Management Console,
select the client you want to backup and set the
**enable backup job** checkbox to true, as shown in
the screenshot below.

|image|

If the name of the client is **testw1.example.com**,
corresponding configuration files will be generated:

-  */etc/bareos/autogenerated/clients/testw1.example.com.include*

-  */etc/bareos/bareos-dir-export/client/testw1.example.com-fd/bareos-fd.d/director/bareos-dir.conf*

Generated configuration files under
*/etc/bareos/bareos-dir-export/client/* are
intended for the target systems. After you have
:ref:`installed the Bareos client on the target system SecondClient`,
copy the generated client configuration over to the client and save it
to following directories:

-  on Linux: :raw-latex:`\path`\|/etc/bareos/bareos-fd.d/director/\|

-  on Windows:
   :raw-latex:`\path`\|C::raw-latex:`\Program`Files:raw-latex:`\Bareos`:raw-latex:`\bareos`-fd.d/director/\|

.. raw:: latex

   \begin{commands}{copy client configuration from the server to the testw1.example.com client (Linux)}
   root@ucs:~# <input>CLIENTNAME=testw1.example.com</input>
   root@ucs:~# <input>scp /etc/bareos/bareos-dir-export/client/${CLIENTNAME}-fd/bareos-fd.d/director/*.conf root@${CLIENTNAME}:/etc/bareos/bareos-fd.d/director/</input>
   \end{commands}

Background
^^^^^^^^^^

The settings for each job resource are defined by the template files you
see below:

The files

-  */etc/bareos/autogenerated/clients/generic.template*

-  */etc/bareos/autogenerated/clients/windows.template*

are used as templates for new clients. For Windows clients the file
*windows.template* is used, the
*generic.template* is used for all other client types.

If you disable the Bareos backup for a client, the client will not be
removed from the configuration files. Only the backup job will be set
inactive.

If you add three client, your client directory will look similar to
this:

.. raw:: latex

   \begin{commands}{}
   root@ucs:/etc/bareos/autogenerated/clients# <input>ls -l</input>
   -rw-r--r-- 1 root root 430 16. Mai 15:15 generic.template
   -rw-r----- 1 root bareos 513 21. Mai 14:46 testw1.example.com.include
   -rw-r----- 1 root bareos 518 21. Mai 14:49 testw2.example.com.include
   -rw-r----- 1 root bareos 518 16. Mai 18:17 testw3.example.com.include
   -rw-r--r-- 1 root root 439 16. Mai 15:15 windows.template
   \end{commands}

The client configuration file contains, as you can see below, the client
connection and the job information:

.. raw:: latex

   \begin{commands}{}
   root@ucs:/etc/bareos/autogenerated/clients# <input>cat testw2.example.com.include</input>
   Client {
    Name = "testw2.example.com-fd"
    Address = "testw2.example.com"
    Password = "DBLtVnRKq5nRUOrnB3i3qAE38SiDtV8tyhzXIxqR"
   }

   Job {
    Name = "Backup-testw2.example.com" # job name
    Client = "testw2.example.com-fd" # client name
    JobDefs = "DefaultJob" # job definition for the job
    FileSet = "Windows All Drives" # FileSet (data which is backed up)
    Schedule = "WeeklyCycle" # schedule for the backup tasks
    Enabled = "Yes" #this is the ressource which is toggled on/off by enabling or disabling a backup from the univention gui
   }
   \end{commands}

Bareos :math:`<` 16.2.0
^^^^^^^^^^^^^^^^^^^^^^^

Older versions of Bareos handle generating the client configuration
similar, but not identical:

If the name of the client is **testw1.example.com**,
corresponding configuration files will be generated/adapted:

-  creates
   */etc/bareos/autogenerated/fd-configs/testw1.example.com.conf*

-  creates
   */etc/bareos/autogenerated/clients/testw1.example.com.include*

-  extends */etc/bareos/autogenerated/clients.include*

Here the files intended for the target systems are generated under
*/etc/bareos/autogenerated/fd-configs/* and they
do not only definr a director resource, but are full configuration files
for the client. After you have
:ref:`installed the Bareos client on the target system SecondClient`,
copy the generated client configuration over to the client and save it
to

-  on Linux: :raw-latex:`\path`\|/etc/bareos/bareos-fd.conf\|

-  on Windows:
   :raw-latex:`\path`\|C::raw-latex:`\Program`Files:raw-latex:`\Bareos`:raw-latex:`\bareos`-fd.conf\|

.. raw:: latex

   \begin{commands}{copy client configuration from the server to the testw1.example.com client (Linux)}
   root@ucs:~# <input>CLIENTNAME=testw1.example.com</input>
   root@ucs:~# <input>scp /etc/bareos/autogenerated/fd-configs/${CLIENTNAME}.conf root@${CLIENTNAME}:/etc/bareos/bareos-fd.conf</input>
   \end{commands}

Debian.org / Ubuntu Universe
----------------------------


.. index:: 
   triple: General; Platform!Debian; Debian.org

.. index:: 
   triple: General; Platform!Debian; 8

.. index:: 
   triple: General; Platform!Ubuntu; Universe

.. index:: 
   triple: General; Platform!Ubuntu!Universe; 15.04
.. _sec:DebianOrg:

The distributions of Debian :math:`>=` 8 include a version of Bareos.
Ubuntu Universe :math:`>=` 15.04 does also include these packages.

In the further text, these version will be named
**Bareos (Debian.org)** (also for the Ubuntu Universe
version, as this is based on the Debian version).

Limitations of the Debian.org/Ubuntu Universe version of Bareos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Debian.org does not include the libfastlz compression library and
   therefore the Bareos (Debian.org) packages do not offer the fileset
   options **compression=LZFAST**,
   **compression=LZ4** and
   **compression=LZ4HC**.

-  Debian.org prefers that Bareos (Debian.org) is linked against GnuTLS
   instead of OpenSSL. Therefore, the Bareos (Debian.org) package only
   support :ref:`sec:TransportEncryption` but no
   :ref:`DataEncryption`.

-  Debian.org does not include the **bareos-webui**
   package.

Mac OS X
--------


.. index:: 
   triple: General; Platform!Mac; OS X
.. _sec:macosx:

Bareos for MacOS X is available either

-  via the https://brew.sh/
   (http://formulae.brew.sh/formula/bareos-client) or

-  as pkg file from
   http://download.bareos.org/bareos/release/latest/MacOS/.

However, you have to choose upfront, which client you want to use.
Otherwise conflicts do occur.

Both packages contain the  |bareosFd| and
:command:`bconsole`.

Installing the Bareos Client as PKG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Installation; MacOS

The Bareos installer package for Mac OS X contains the
 |bareosFd| for Mac OS X 10.5 or later.

On your local Mac, you must be an admin user. The main user is an admin
user.

Download the *bareos-client*.pkg* installer package
from http://download.bareos.org/bareos/release/latest/MacOS/.

Find the .pkg you just downloaded. Install the .pkg by holding the CTRL
key, left-clicking the installer and choosing
:raw-latex:`\bquote{open}`.

Follow the directions given to you and finish the installation.

Configuration
~~~~~~~~~~~~~

To make use of your  |bareosFd| on your system, it is required
to configure the  |bareosDir| and the local
 |bareosFd| .

Configure the server-side by follow the instructions at
:ref:`sec:AddAClient`.

After configuring the server-side you can either transfer the necessary
configuration file using following command or configure the client
locally.

:raw-latex:`\subsubsubsection{Option 1: Copy the director resource from the Bareos Director to the Client}`

Assuming your client has the DNS entry
**client2.example.com** and has been added to
 |bareosDir| as
:raw-latex:`\resourcename{bareos-dir}{client}{client2-fd}`:

.. raw:: latex

   \begin{commands}{}
   scp /etc/bareos/bareos-dir-export/client/client2-fd/bareos-fd.d/director/bareos-dir.conf root@client2.example.com:/usr/local/etc/bareos/bareos-fd.d/director/
   \end{commands}

This differs in so far, as on Linux the configuration files are located
under :raw-latex:`\path`\|/etc/bareos/\|, while on MacOS they are
located at :raw-latex:`\path`\|/usr/local/etc/bareos/\|.

:raw-latex:`\subsubsubsection{Option 2: Edit the director resource on the Client}`

Alternatively, you can edit the file
:raw-latex:`\path`\|/usr/local/etc/bareos/bareos-fd.d/director/bareos-dir.conf\|.

This can be done by right-clicking the finder icon in your task bar,
select :raw-latex:`\bquote{Go to folder ...}` and paste
:raw-latex:`\path`\|/usr/local/etc/bareos/bareos-fd.d/director/\|.

Select the :raw-latex:`\path`\|bareos-dir.conf\| file and open it.

Alternatively you can also call following command on the command
console:

.. raw:: latex

   \begin{commands}{}
   open -t /usr/local/etc/bareos/bareos-fd.d/director/bareos-dir.conf
   \end{commands}

The file should look similar to this:

.. raw:: latex

   \begin{bareosConfigResource}{bareos-fd}{director}{bareos-dir}
   Director {
     Name = bareos-dir
     Password = "SOME_RANDOM_PASSWORD"
     Description = "Allow the configured Director to access this file daemon."
   }
   \end{bareosConfigResource}

Set this client-side password to the same value as given on the
server-side.


.. warning:: 
  The configuration file contains passwords and therefore must not be accessible for any users except admin users.

Restart bareos-fd after changing the configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The bareos-fd must be restarted to reread its configuration:

.. raw:: latex

   \begin{commands}{Restart the \bareosFd}
   sudo launchctl stop  org.bareos.bareos-fd
   sudo launchctl start org.bareos.bareos-fd
   \end{commands}

Verify that the Bareos File Daemon is working
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open the :command:`bconsole` on your
 |bareosDir| and check the status of the client with

.. raw:: latex

   \begin{bconfig}{}
   *<input>status client=client2-fd</input>
   \end{bconfig}

In case, the client does not react, following command are useful the
check the status:

.. raw:: latex

   \begin{commands}{Verify the status of \bareosFd}
   # check if bareos-fd is started by system:
   sudo launchctl list org.bareos.bareos-fd

   # get process id (PID) of bareos-fd
   pgrep bareos-fd

   # show files opened by bareos-fd
   sudo lsof -p `pgrep bareos-fd`

   # check what process is listening on the \bareosFd port
   sudo lsof -n -iTCP:9102 | grep LISTEN
   \end{commands}

You can also manually start bareos-fd in debug mode by:

.. raw:: latex

   \begin{commands}{Start \bareosFd in debug mode}
   sudo /usr/local/sbin/bareos-fd -f -d 100
   \end{commands}

.. |image| image:: \idir univention-configuration-registry-settings
   :width: 100.0%
.. |image| image:: \idir univention-ucs-overview-administration
   :width: 80.0%
.. |image| image:: \idir univention-client-job-activation
   :width: 80.0%
