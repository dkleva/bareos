This chapter addresses the installation process of the
|bareosWebui| .

Since 15.2.0
|bareosWebui| is part of the Bareos project and available for
a number of platforms.

|image|

Features
========

-  Intuitive web interface

-  Multilinugual

-  Can access multiple directors and catalogs

-  Individual accounts and ACL support via Bareos restricted named
   consoles

-  Tape Autochanger management, with the possibility to label,
   import/export media and update your autochanger slot status

-  Temporarly enable or disable jobs, clients and schedules and also see
   their current state

-  Show

   -  Detailed information about Jobs, Clients, Filesets, Pools,
      Volumes, Storages, Schedules, Logs and Director messages

   -  Filedaemon, Storage- and Director updates

   -  Client, Director, Storage and Scheduler status

-  Backup Jobs

   -  Start, cancel, rerun and restore from.

   -  Show the file list of backup jobs

-  Restore files by browsing through a filetree of your backup jobs.

   -  Merge your backup jobs history and filesets of a client or use a
      single backup job for restore.

   -  Restore files to a different client instead of the origin

-  bconsole interface (limited to non-interactive commands)

System Requirements
===================

-  A platform, for which the **bareos-webui** package
   is available, see :ref:**sec:BareosPackages**.

-  A working Bareos environment.

-  |bareosDir| version :math:**>=**
   |bareosWebui| version.

-  The |bareosWebui| can be installed on any host. It does
   not have to be installed on the same as the |bareosDir| .

-  The default installation uses an Apache webserver with mod-rewrite,
   mod-php and mod-setenv.

*-  PHP :math:`>`* = 5.3.23

-  On SUSE Linux Enterprise 12 you need the additional SUSE Linux
   Enterprise Module for Web Scripting 12.

Version :math:**<** 16.2
----------------------

|bareosWebui| 16.2.4
incorporates the required Zend Framework 2 components, no extra Zend
Framework installation is required. For older versions of
**bareos-webui**, you must install Zend Framework
separately. Unfortunately, not all distributions offer Zend Framework 2
packages. The following list shows where to get the Zend Framework 2
package:

-  RHEL, CentOS

   -  https://fedoraproject.org/wiki/EPEL

   -  https://apps.fedoraproject.org/packages/php-ZendFramework2

-  Fedora

   -  https://apps.fedoraproject.org/packages/php-ZendFramework2

-  SUSE, Debian, Ubuntu

   -  http://download.bareos.org/bareos

Also be aware, that older versions of |bareosDir| do not
support the :ref:**sec:SubdirectoryConfigurationScheme**
and therefore Bareos configuration resource files must be included
manually.

Installation
============

Adding the Bareos Repository
----------------------------

If not already done, add the Bareos repository that is matching your
Linux distribution. Please have a look at the chapter
:ref:**sec:InstallBareosPackages** for more information on
how to achieve this.

Install the bareos-webui package
--------------------------------

After adding the repository simply install the bareos-webui package via
your package manager.

-  RHEL, CentOS and Fedora

   .. raw:: latex

*      *begin{commands}{}
      yum install bareos-webui
*      *end{commands}

   or

   .. raw:: latex

*      *begin{commands}{}
      dnf install bareos-webui
*      *end{commands}

-  SUSE Linux Enterprise Server (SLES), openSUSE

   .. raw:: latex

*      *begin{commands}{}
      zypper install bareos-webui
*      *end{commands}

-  Debian, Ubuntu

   .. raw:: latex

*      *begin{commands}{}
      apt-get install bareos-webui
*      *end{commands}

Minimal Configuration
---------------------

This assumes, |bareosDir| and |bareosWebui| are
installed on the same host.

#. If you are using SELinux, allow HTTPD scripts and modules make
   network connections:

   .. raw:: latex

*      *begin{commands}{}
      setsebool -P httpd_can_network_connect on
*      *end{commands}

   For details, see :ref:**sec:webui-selinux**.

#. Restart Apache (to load configuration provided by bareos-webui, see
   :ref:**sec:webui-apache**)

#. .. _item:webui-create-user: Use
   :kbd:**bconsole** to create a user with name
*   **admin}` and password :raw-latex:`*name{secret** and
   permissions defined in
*   :raw-latex:`*resourcename{Dir}{Profile}{webui-admin}**:

   .. raw:: latex

*      *begin{bconsole}{add a named console}
      *<input>configure add console name=admin password=secret profile=webui-admin</input>
*      *end{bconsole}

   Of course, you can choose other names and passwords. For details, see
   :ref:**sec:webui-console**.

#. Login to http://HOSTNAME/bareos-webui with username and password as
*   created in :raw-latex:`*ref{item:webui-create-user}**.

Configuration Details
---------------------

Create a restricted consoles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There is not need, that |bareosWebui| itself provide a user
management. Instead it uses so named
*:raw-latex:`*resourcetype{Dir}{Console}** defined in the
|bareosDir| . You can have multiple consoles with different
names and passwords, sort of like multiple users, each with different
privileges.

*At least one :raw-latex:`*resourcetype{Dir}{Console}** is required to use
the |bareosWebui| .

To allow a user with name **admin** and password
**secret** to access the |bareosDir| with
permissions defined in the
*:raw-latex:`*resourcename{Dir}{Profile}{webui-admin}** (see
:ref:**sec:webui-profile**), either

-  create a file
   */etc/bareos/bareos-dir.d/console/admin.conf* with
   following content:

   .. raw:: latex

*      *begin{bareosConfigResource}{bareos-dir}{console}{admin}
      Console {
        Name = "admin"
        Password = "secret"
        Profile = "webui-admin"
      }
*      *end{bareosConfigResource}

   To enable this, reload or restart your |bareosDir| .

-  or use the :kbd:**bconsole**:

   .. raw:: latex

*      *begin{bconsole}{add console}
      *<input>configure add console name=admin password=secret profile=webui-admin</input>
*      *end{bconsole}

For details, please read :ref:**DirectorResourceConsole**.

Configuration of profile resources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The package **bareos-webui** comes with a predefined
profile for |bareosWebui| :
*:raw-latex:`*resourcename{Dir}{Profile}{webui-admin}**.

If your |bareosWebui| is installed on another system then the
|bareosDir| , you have to copy the profile to the
|bareosDir| .

This is the default profile, giving access to all Bareos resources and
allowing all commands used by the |bareosWebui| :

.. raw:: latex

*   *begin{bareosConfigResource}{bareos-dir}{profile}{webui-admin}
   Profile {
     Name = webui-admin
     CommandACL = !.bvfs_clear_cache, !.exit, !.sql, !configure, !create, !delete, !purge, !sqlquery, !umount, !unmount, *all*
     Job ACL = *all*
     Schedule ACL = *all*
     Catalog ACL = *all*
     Pool ACL = *all*
     Storage ACL = *all*
     Client ACL = *all*
     FileSet ACL = *all*
     Where ACL = *all*
     Plugin Options ACL = *all*
   }
*   *end{bareosConfigResource}

*The :raw-latex:`*resourcetype{Dir}{Profile}** itself does not give any
access to the |bareosDir| , but can be used by
*:raw-latex:`*resourcetype{Dir}{Console}**, which do give access to the
|bareosDir| , see :ref:**sec:webui-console**.

For details, please read :ref:**DirectorResourceProfile**.

SELinux
~~~~~~~


.. index:: 
   triple: General; SELinux; bareos-webui

To use |bareosDir| on a system with SELinux enabled,
permission must be given to HTTPD to make network connections:

.. raw:: latex

*   *begin{commands}{}
   setsebool -P httpd_can_network_connect on
*   *end{commands}

Configure your Apache Webserver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Apache; bareos-webui
.. _sec:webui-apache:

The package **bareos-webui** provides a default
configuration for Apache. Depending on your distribution, it is
installed at */etc/apache2/conf.d/bareos-webui.conf*,
*/etc/httpd/conf.d/bareos-webui.conf* or
*/etc/apache2/available-conf/bareos-webui.conf*.

The required Apache modules, **setenv**,
***rewrite}` and :raw-latex:`*argument{php** are
enabled via package postinstall script. However, after installing the
**bareos-webui** package, you need to restart your
Apache webserver manually.

Configure your /etc/bareos-webui/directors.ini
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. index:: 
   triple: General; Configuration; WebUI
.. _sec:webui-configuration-files:

Configure your directors in
*/etc/bareos-webui/directors.ini* to match your
settings.

The configuration file
*/etc/bareos-webui/directors.ini* should look similar
to this:

.. raw:: latex

*   *begin{bconfig}{/etc/bareos-webui/directors.ini}
   ;
   ; Bareos WebUI Configuration File
   ;
   ; File: /etc/bareos-webui/directors.ini
   ;

   ;------------------------------------------------------------------------------
   ; Section localhost-dir
   ;------------------------------------------------------------------------------
   [localhost-dir]

   ; Enable or disable section. Possible values are "yes" or "no", the default is "yes".
   enabled = "yes"

   ; Fill in the IP-Address or FQDN of you director.
   diraddress = "localhost"

   ; Default value is 9101
   dirport = 9101

   ; Set catalog to explicit value if you have multiple catalogs
   ;catalog = "MyCatalog"

   ; TLS verify peer
   ; Possible values: true or false
   tls_verify_peer = false

   ; Server can do TLS
   ; Possible values: true or false
   server_can_do_tls = false

   ; Server requires TLS
   ; Possible values: true or false
   server_requires_tls = false

   ; Client can do TLS
   ; Possible values: true or false
   client_can_do_tls = false

   ; Client requires TLS
   ; Possible value: true or false
   client_requires_tls = false

   ; Path to the certificate authority file
   ; E.g. ca_file = "/etc/bareos-webui/tls/BareosCA.crt"
   ;ca_file = ""

   ; Path to the cert file which needs to contain the client certificate and the key in PEM encoding
   ; E.g. ca_file = "/etc/bareos-webui/tls/restricted-named-console.pem"
   ;cert_file = ""

   ; Passphrase needed to unlock the above cert file if set
   ;cert_file_passphrase = ""

   ; Allowed common names
   ; E.g. allowed_cns = "host1.example.com"
   ;allowed_cns = ""

   ;------------------------------------------------------------------------------
   ; Section another-host-dir
   ;------------------------------------------------------------------------------
   [another-host-dir]
   enabled = "no"
   diraddress = "192.168.120.1"
   dirport = 9101
   ;catalog = "MyCatalog"
   ;tls_verify_peer = false
   ;server_can_do_tls = false
   ;server_requires_tls = false
   ;client_can_do_tls = false
   ;client_requires_tls = false
   ;ca_file = ""
   ;cert_file = ""
   ;cert_file_passphrase = ""
   ;allowed_cns = ""

*   *end{bconfig}

You can add as many directors as you want, also the same host with a
different name and different catalog, if you have multiple catalogs.

Configure your /etc/bareos-webui/configuration.ini
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since
16.2.2
you are able to configure some parameters of the
|bareosWebui| to your needs.

.. raw:: latex

*   *begin{bconfig}{/etc/bareos-webui/configuration.ini}
   ;
   ; Bareos WebUI Configuration File
   ;
   ; File: /etc/bareos-webui/configuration.ini
   ;

   ;------------------------------------------------------------------------------
   ; SESSION SETTINGS
   ;------------------------------------------------------------------------------
   ;
   [session]
   ; Default: 3600 seconds
   timeout=3600

   ;------------------------------------------------------------------------------
   ; DASHBOARD SETTINGS
   ;------------------------------------------------------------------------------
   [dashboard]
   ; Autorefresh Interval
   ; Default: 60000 milliseconds
   autorefresh_interval=60000

   ;------------------------------------------------------------------------------
   ; TABLE SETTINGS
   ;------------------------------------------------------------------------------
   [tables]
   ; Possible values for pagination
   ; Default: 10,25,50,100
   pagination_values=10,25,50,100

   ; Default number of rows per page
   ; for possible values see pagination_values
   ; Default: 25
   pagination_default_value=25

   ; State saving - restore table state on page reload.
   ; Default: false
   save_previous_state=false

   ;------------------------------------------------------------------------------
   ; VARIOUS SETTINGS
   ;------------------------------------------------------------------------------
   [autochanger]
   ; Pooltype for label to use as filter.
   ; Default: none
   labelpooltype=scratch

*   *end{bconfig}

Upgrade from 15.2 to 16.2
=========================

Console/Profile changes
-----------------------

The |bareosWebui| Director profile shipped with Bareos 15.2
*(:raw-latex:`*resourcename{Dir}{Profile}{webui}** in the file
*/etc/bareos/bareos-dir.d/webui-profiles.conf*) is not
sufficient to use the |bareosWebui| 16.2. This has several
reasons:

*#. The handling of :raw-latex:`*dt{Acl}**s is more strict in Bareos 16.2
   then it has been in Bareos 15.2. Substring matching is no longer
   enabled, therefore you need to change :kbd:**.bvfs_***
   to :kbd:**.bvfs_.*** in your
*   :raw-latex:`*linkResourceDirective{Dir}{Profile}{Command ACL}** to
   have a proper regular expression. Otherwise the restore module won’t
   work any longer, especially the file browser.

#. The |bareosWebui| 16.2 uses following additional commands:

   -  .help

   -  .schedule

   -  .pools

   -  import

   -  export

   -  update

   -  release

   -  enable

   -  disable

If you used an unmodified
*/etc/bareos/bareos-dir.d/webui-profiles.conf* file,
the easiest way is to overwrite it with the new profile file
*/etc/bareos/bareos-dir.d/profile/webui-admin.conf*.
*The new :raw-latex:`*resourcename{Dir}{Profile}{webui-admin}** allows all
commands, except of the dangerous ones, see
:ref:**sec:webui-profile**.

directors.ini
-------------

Since
16.2.0
it is possible to work with different catalogs. Therefore the catalog
parameter has been introduced. If you don’t set a catalog explicitly the
*default :raw-latex:`*resourcename{Dir}{Catalog}{MyCatalog}** will be
used. Please see :ref:**sec:webui-configuration-files**
for more details.

configuration.ini
-----------------

Since 16.2 the |bareosWebui| introduced an additional
configuration file besides the directors.ini file named
configuration.ini where you are able to adjust some parameters of the
webui to your needs. Please see
:ref:**sec:webui-configuration-files** for more details.

Additional information
======================

NGINX
-----


.. index:: 
   triple: General; nginx; bareos-webui

If you prefer to use |bareosWebui| on Nginx with php5-fpm
instead of Apache, a basic working configuration could look like this:

*:raw-latex:`*todo{repair manually}**

This will make the |bareosWebui| accessible at
http://bareos:9100/ (assuming your DNS resolve the hostname
**bareos** to the NGINX server).

*.. |image| image:: *idir bareos-webui-jobs
   :width: 80.0%





















