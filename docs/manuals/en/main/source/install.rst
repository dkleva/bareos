If you are like me, you want to get Bareos running immediately to get a
feel for it, then later you want to go back and read about all the
details. This chapter attempts to accomplish just that: get you going
quickly without all the details.

Bareos comes prepackaged for a number of Linux distributions. So the
easiest way to get to a running Bareos installation, is to use a
platform where prepacked Bareos packages are available. Additional
information can be found in the chapter
:ref:`Operating Systems SupportedOSes`.

If Bareos is available as a package, only 4 steps are required to get to
a running Bareos system:

#. :ref:`sec:AddSoftwareRepository`

#. :ref:`sec:InstallBareosPackages`

#. :ref:`sec:CreateDatabase`

#. :ref:`sec:StartDaemons`

This will start a very basic Bareos installation which will regularly
backup a directory to disk. In order to fit it to your needs, you’ll
have to adapt the configuration and might want to backup other clients.

Decide about the Bareos release to use
======================================

-  http://download.bareos.org/bareos/release/latest/

You’ll find Bareos binary package repositories at
http://download.bareos.org/. The latest stable released version is
available at http://download.bareos.org/bareos/release/latest/.

The public key to verify the repository is also in repository directory
(*Release.key* for Debian based distributions,
*repodata/repomd.xml.key* for RPM based
distributions).

Section :ref:`sec:InstallBareosPackages` describes how
to add the software repository to your system.

Decide about the Database Backend
=================================

Bareos offers the following database backends:

-  PostgreSQL by package
   **bareos-database-postgresql**. This is the
   recommended backend.

-  MariaDB/MySQL by package **bareos-database-mysql**

-  | Sqlite by package **bareos-database-sqlite3**
   | 
.. warning:: 
  The Sqlite backend is only intended for testing, not for productive use.

PostgreSQL
^^^^^^^^^^

is the default backend.

MariaDB/MySQL
^^^^^^^^^^^^^

backend is also included.

Sqlite
^^^^^^

backend is intended for testing purposes only.

The Bareos database packages have there dependencies only to the
database client packages, therefore the database itself must be
installed manually.

If you do not explicitly choose a database backend, your operating
system installer will choose one for you. The default should be
PostgreSQL, but depending on your operating system and the already
installed packages, this may differ.

Install the Bareos Software Packages
====================================

The package **bareos** is only a meta package, that
contains dependencies to the main components of Bareos, see
:ref:`sec:BareosPackages`. If you want to setup a
distributed environment (like one Director, separate database server,
multiple Storage daemons) you have to choose the corresponding Bareos
packages to install on each hosts instead of just installing the
**bareos** package.

Install on RedHat based Linux Distributions
-------------------------------------------

RHEL\ :math:`\ge`\ 7, CentOS\ :math:`\ge`\ 7, Fedora
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Platform; RHEL

.. index:: 
   triple: General; Platform; CentOS

.. index:: 
   triple: General; Platform; Fedora

Bareos 15.2.0
requires the :ref:`Jansson library jansson` package. On
RHEL 7 it is available through the RHEL Server Optional channel. On
CentOS 7 and Fedora is it included on the main repository.

.. raw:: latex

   \begin{commands}{Bareos installation on RHEL $\ge$ 7 / CentOS $\ge$ 7 / Fedora}
   #
   # define parameter
   #

   DIST=RHEL_7
   # or
   # DIST=CentOS_7
   # DIST=Fedora_26
   # DIST=Fedora_25

   RELEASE=release/17.2/
   # or
   # RELEASE=release/latest/
   # RELEASE=experimental/nightly/

   # add the Bareos repository
   URL=http://download.bareos.org/bareos/$RELEASE/$DIST
   wget -O /etc/yum.repos.d/bareos.repo $URL/bareos.repo

   # install Bareos packages
   yum install bareos bareos-database-postgresql
   \end{commands}
   \hide{$}

   \subsubsection{RHEL 6, CentOS 6}
   \index[general]{Platform!RHEL!6}
   \index[general]{Platform!CentOS!6}

   Bareos \sinceVersion{dir}{requires!jansson}{15.2.0} requires the \ilink{Jansson library}{jansson} package.
   This package is available on \elink{EPEL}{https://fedoraproject.org/wiki/EPEL} 6. Make sure, it is available on your system.

   \begin{commands}{Bareos installation on RHEL $\ge$ 6 / CentOS $\ge$ 6}
   #
   # add EPEL repository, if not already present.
   # Required for the jansson package.
   #
   rpm -Uhv https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm

   #
   # define parameter
   #

   DIST=RHEL_6
   # DIST=CentOS_6

   RELEASE=release/17.2/
   # or
   # RELEASE=release/latest/
   # RELEASE=experimental/nightly/

   # add the Bareos repository
   URL=http://download.bareos.org/bareos/$RELEASE/$DIST
   wget -O /etc/yum.repos.d/bareos.repo $URL/bareos.repo

   # install Bareos packages
   yum install bareos bareos-database-postgresql
   \end{commands}



RHEL 5
~~~~~~


.. index:: 
   triple: General; Platform!RHEL; 5 yum in RHEL 5/CentOS 5 has
slightly different behaviour as far as dependency resolving is
concerned: it sometimes install a dependent package after the one that
has the dependency defined. To make sure that it works, install the
desired Bareos database backend package first in a separate step:

.. raw:: latex

   \begin{commands}{Bareos installation on RHEL 5 / CentOS 5}
   #
   # define parameter
   #

   DIST=RHEL_5

   RELEASE=release/17.2/
   # or
   # RELEASE=release/latest/
   # RELEASE=experimental/nightly/

   # add the Bareos repository
   URL=http://download.bareos.org/bareos/$RELEASE/$DIST
   wget -O /etc/yum.repos.d/bareos.repo $URL/bareos.repo

   # install Bareos packages
   yum install bareos-database-postgresql
   yum install bareos
   \end{commands}
   \hide{$}

   \subsection{Install on SUSE based Linux Distributions}

   \subsubsection{SUSE Linux Enterprise Server (SLES), openSUSE}
   \index[general]{Platform!SLES}
   \index[general]{Platform!openSUSE}

   \begin{commands}{Bareos installation on SLES / openSUSE}
   #
   # define parameter
   #

   DIST=SLE_12_SP3
   # or
   # DIST=SLE_12_SP2
   # DIST=SLE_12_SP1
   # DIST=SLE_11_SP4
   # DIST=openSUSE_Leap_42.3
   # DIST=openSUSE_Leap_42.2

   RELEASE=release/17.2/
   # or
   # RELEASE=release/latest/
   # RELEASE=experimental/nightly/

   # add the Bareos repository
   URL=http://download.bareos.org/bareos/$RELEASE/$DIST
   zypper addrepo --refresh $URL/bareos.repo

   # install Bareos packages
   zypper install bareos bareos-database-postgresql
   \end{commands}



Install on Debian based Linux Distributions
-------------------------------------------

Debian / Ubuntu
~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Platform; Debian

.. index:: 
   triple: General; Platform; Ubuntu

Bareos 15.2.0
requires the :ref:`Jansson library jansson` package. On
Ubuntu is it available in Ubuntu Universe. In Debian, is it included in
the main repository.

.. raw:: latex

   \begin{commands}{Bareos installation on Debian / Ubuntu}
   #
   # define parameter
   #

   DIST=Debian_9.0
   # or
   # DIST=Debian_8.0
   # DIST=xUbuntu_16.04
   # DIST=xUbuntu_14.04
   # DIST=xUbuntu_12.04

   RELEASE=release/17.2/
   # or
   # RELEASE=release/latest/
   # RELEASE=experimental/nightly/

   URL=http://download.bareos.org/bareos/$RELEASE/$DIST

   # add the Bareos repository
   printf "deb $URL /\n" > /etc/apt/sources.list.d/bareos.list

   # add package key
   wget -q $URL/Release.key -O- | apt-key add -

   # install Bareos packages
   apt-get update
   apt-get install bareos bareos-database-postgresql
   \end{commands}

If you prefer using the versions of Bareos directly integrated into the
distributions, please note that there are some differences, see
:ref:`sec:DebianOrgLimitations`.

Install on Univention Corporate Server
--------------------------------------


.. index:: 
   triple: General; Platform; Univention Corporate Server

Bareos offers additional functionality and integration into an
Univention Corporate Server environment. Please follow the intructions
in :ref:`sec:UniventionCorporateServer`.

If you are not interested in this additional functionality, the commands
described in :ref:`sec:InstallBareosPackagesDebian` will
also work for Univention Corporate Servers.

Prepare Bareos database
=======================

We assume that you have already your database installed and basically
running. Using the PostgreSQL database backend is recommended.

The easiest way to set up a database is using an system account that
have passwordless local access to the database. Often this is the user
**root** for MySQL and the user
**postgres** for PostgreSQL.

For details, see chapter :ref:`CatMaintenanceChapter`.

Debian based Linux Distributions
--------------------------------

Since Bareos
14.2.0 the
Debian (and Ubuntu) based packages support the
**dbconfig-common** mechanism to create and update
the Bareos database.

Follow the instructions during install to configure it according to your
needs.

|image| |image|

If you decide not to use **dbconfig-common**
(selecting **<No>** on the initial dialog), follow
the instructions for
:ref:`sec:CreateDatabaseOtherDistributions`.

The selectable database backends depend on the
**bareos-database-*** packages installed.

For details see :ref:`sec:dbconfig`.

Other Platforms
---------------

PostgreSQL
~~~~~~~~~~

If your are using PostgreSQL and your PostgreSQL administration user is
**postgres** (default), use following commands:

.. raw:: latex

   \begin{commands}{Setup Bareos catalog with PostgreSQL}
   su postgres -c /usr/lib/bareos/scripts/create_bareos_database
   su postgres -c /usr/lib/bareos/scripts/make_bareos_tables
   su postgres -c /usr/lib/bareos/scripts/grant_bareos_privileges
   \end{commands}

MySQL/MariaDB
~~~~~~~~~~~~~

Make sure, that **root** has direct access to the local
MySQL server. Check if the command :command:`mysql` connects
to the database without defining the password. This is the default on
RedHat and SUSE distributions. On other systems (Debian, Ubuntu), create
the file *~/.my.cnf* with your authentication
informations:

.. raw:: latex

   \begin{config}{MySQL credentials file .my.cnf}
   [client]
   host=localhost
   user=root
   password=<input>YourPasswordForAccessingMysqlAsRoot</input>
   \end{config}

It is recommended, to secure the Bareos database connection with a
password. See
:ref:`Catalog Maintenance -- MySQL catalog-maintenance-mysql`
about how to archieve this. For testing, using a password-less MySQL
connection is probable okay. Setup the Bareos database tables by
following commands:

.. raw:: latex

   \begin{commands}{Setup Bareos catalog with MySQL}
   /usr/lib/bareos/scripts/create_bareos_database
   /usr/lib/bareos/scripts/make_bareos_tables
   /usr/lib/bareos/scripts/grant_bareos_privileges
   \end{commands}

As some Bareos updates require a database schema update, therefore the
file */root/.my.cnf* might also be useful in the
future.

Start the daemons
=================

.. raw:: latex

   \begin{commands}{Start the Bareos Daemons}
   service bareos-dir start
   service bareos-sd start
   service bareos-fd start
   \end{commands}

You will eventually have to allow access to the ports 9101-9103, used by
Bareos.

Now you should be able to access the director using the bconsole.

When you want to use the bareos-webui, please refer to the chapter
:ref:`sec:install-webui`.

.. |image| image:: \idir dbconfig-1-enable
   :width: 45.0%
.. |image| image:: \idir dbconfig-2-select-database-type
   :width: 45.0%
