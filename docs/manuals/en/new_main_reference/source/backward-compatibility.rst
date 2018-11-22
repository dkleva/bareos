Backward Compatibility
======================


.. index:: 
   triple: General; Compatibility; Backward
.. _backward-compability:

Tape Formats
------------


.. index:: 
   triple: General; Tape; Format
.. _backward-compability-tape-format:

One of the major goals of Backup softare is to ensure that you can
restore tapes (the word tape should also include disk volumes) that you
wrote years ago. This means that each new version of the software should
be able to read old format tapes. The first problem you will have is to
ensure that the hardware is still working some years down the road, and
the second problem will be to ensure that the media will still be good,
then your OS must be able to interface to the device, and finally Bareos
must be able to recognize old formats. All the problems except the last
are ones that we cannot solve, but by careful planning you can.

Since the very beginning of Bacula (January 2000) until today (2015),
there have been three major Bacula/Bareos tape formats. The second
format was introduced in Bacula version 1.27 in November of 2002. Bareos
has been required to adapt the tape format to avoid potential trademark
issues, but is able to read also the old Bacula tape formats.

Though the tape format is basically fixed, the kinds of data that we can
put on the tapes are extensible, and that is how we added new features
such as ACLs, Win32 data, encrypted data, ... Obviously, an older
version of Bacula/Bareos would not know how to read these newer data
streams, but each newer version of Bareos should know how to read all
the older streams.

Compatibility between Bareos and Bacula
---------------------------------------


.. index:: 
   triple: General; Compatibility; Bacula
.. index:: General; Bacula}` :raw-latex:`\label{compat-bacula 

A Director and a Storage Daemon should (must) always run at the same
version. This is true for Bareos as well as for Bacula. It is not
possible to mix these components. This is because the protocol between
Director and Storage Daemon itself is not versioned (also true for
Bareos and Bacula). If you want to be able to switch back from Bareos to
Bacula after using a Bareos director and storage daemon you have to
enable the compatible mode in the Bareos storage daemon to have it write
the data in the same format as the Bacula storage daemon.

The  |bareosFd| is compatible with all version of the Bacula
director (tested with version 5.2.13 and lower) when you enable the
compatible mode in the configuration of the  |bareosFd| . The
compatible option was set by default in Bareos :math:`<` 15.2.0, and is
disabled by default since
15.2.0.

To be sure this is enabled you can explicitly set the compatible option:

:raw-latex:`\resourceDirectiveValue{Fd}{Client}{Compatible}{True}`

A  |bareosDir| can only talk to Bacula file daemons of version
2.0 or higher. Through a change in the Bacula network protocols, it is
currently not possible to use a Bacula file daemon :math:`\ge` 6.0 with
a  |bareosDir| .

These combinations of Bareos and Bacula are know to work together:

+-------------------------------------------+-------------------------------------------+--------------------------------------------------------------------------+---------------+
| **Director**                              | **Storage Daemon**                        | **File Daemon**                                                          | **Remarks**   |
+===========================================+===========================================+==========================================================================+===============+
| :raw-latex:`\textcolor{blue}{Bareos\ }`   | :raw-latex:`\textcolor{blue}{Bareos\ }`   | :raw-latex:`\textcolor{blue}{Bareos\ }`                                  |               |
+-------------------------------------------+-------------------------------------------+--------------------------------------------------------------------------+---------------+
| :raw-latex:`\textcolor{blue}{Bareos\ }`   | :raw-latex:`\textcolor{blue}{Bareos\ }`   | 2.0 :math:`\leq` :raw-latex:`\textcolor{red}{Bacula\ }`\ :math:`<` 6.0   |               |
+-------------------------------------------+-------------------------------------------+--------------------------------------------------------------------------+---------------+
| :raw-latex:`\textcolor{red}{Bacula\ }`    | :raw-latex:`\textcolor{red}{Bacula\ }`    | :raw-latex:`\textcolor{red}{Bacula\ }`                                   |               |
+-------------------------------------------+-------------------------------------------+--------------------------------------------------------------------------+---------------+
| :raw-latex:`\textcolor{red}{Bacula\ }`    | :raw-latex:`\textcolor{red}{Bacula\ }`    | :raw-latex:`\textcolor{blue}{Bareos\ }`(compatibility mode)              |               |
+-------------------------------------------+-------------------------------------------+--------------------------------------------------------------------------+---------------+

Other combinations like Bacula Director with  |bareosSd| will
not work. However this wasn’t even possible with different versions of
bacula-dir and bacula-sd.

Upgrade from Bacula 5.2 to Bareos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. index:: General; Upgrade from Bacula to Bareos 

.. index:: 
   triple: General; Bareos; Upgrading
.. _upgrade-from-bacula-to-bareos:

Upgrade is supported from Bacula version 5.2.x. If you are running any
older version of Bacula, please update to 5.2 first (see Bacula
documentation).


.. warning:: 
  Updating from Bacula $\geq$ 7.0 to Bareos has not been tested.

:raw-latex:`\warning{As Bareos and Bacula packages bring binaries with identical paths and names,
it is on most platforms not possible to install components from both in parallel.
Your package management tool will warn you about this.}`

Rename user and group before upgrading
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To have bareos running without any permission hassle, it is recommended
to rename the user and group **bacula** to the user and
group **bareos** before upgrading. That way, we minimize
the effort for the user to recheck all config files and the rights on
every script/directory etc. involved in the existing setup.

The required commands should look something like this:

.. raw:: latex

   \begin{commands}{}
   usermod  -l bareos bacula
   groupmod -n bareos bacula
   \end{commands}

MySQL
^^^^^

Proceed with the following steps:

-  Stop bacula services

-  Backup your catalog database:

   .. raw:: latex

      \begin{commands}{}
      mysqldump bacula > /tmp/bacula_5.2.sql
      \end{commands}

-  Make the user bareos have the same userid and the group bareos the
   same groupid as the user/group bacula had before. This will solve a
   lot of rights problems.

-  Install Bareos packages

-  Run the update script on the old bacula database:

   .. raw:: latex

      \begin{commands}{}
      export db_name=bacula
      /usr/lib/bareos/update_bareos_tables
      unset db_name
      \end{commands}

-  Backup upgraded DB:

   .. raw:: latex

      \begin{commands}{}
      mysqldump bacula > /tmp/bacula.sql
      \end{commands}

-  Create bareos database:

   .. raw:: latex

      \begin{commands}{}
      /usr/lib/bareos/create_bareos_database
      \end{commands}

-  Insert backuped db into new database:

   .. raw:: latex

      \begin{commands}{}
      cat /tmp/bacula.sql | mysql bareos
      \end{commands}

-  Grant permissions:

   .. raw:: latex

      \begin{commands}{}
      /usr/lib/bareos/grant_mysql_privileges
      \end{commands}

-  Adapt file permissions to bareos, if you have any file storage

-  Adapt configs (not complete)

   -  With bacula the default setting for pid files was
      :raw-latex:`\path`\|/var/run\|, which may not work if the
      bareos-director runs as user bareos. Best way is to comment out
      the entry :command:`Pid Directory = "/var/run"` in
      your director config. Bareos will set a working default value
      (supposed to be :raw-latex:`\path`\|/var/lib/bareos/\|)

PostgreSQL
^^^^^^^^^^

Renaming a postgresql database:

-  Become postgresql user

-  psql template1

   .. raw:: latex

      \begin{commands}{}
      ALTER DATABASE bacula RENAME TO bareos;
      ALTER USER bacula RENAME TO bareos;
      ALTER USER bareos UNENCRYPTED PASSWORD 'password';
      \end{commands}
