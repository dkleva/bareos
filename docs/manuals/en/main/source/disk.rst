.. _DiskChapter:

.. index:: 
   triple: General; Volume; Management
.. index:: General; Disk Volumes 

This chapter presents most all the features needed to do Volume
management. Most of the concepts apply equally well to both tape and
disk Volumes. However, the chapter was originally written to explain
backing up to disk, so you will see it is slanted in that direction, but
all the directives presented here apply equally well whether your volume
is disk or tape.

If you have a lot of hard disk storage or you absolutely must have your
backups run within a small time window, you may want to direct Bareos to
backup to disk Volumes rather than tape Volumes. This chapter is
intended to give you some of the options that are available to you so
that you can manage either disk or tape volumes.

Key Concepts and Resource Records
=================================


.. index:: 
   triple: General; Volume!Management; Key Concepts and Resource Records

Getting Bareos to write to disk rather than tape in the simplest case is
rather easy. In the Storage daemon’s configuration file, you simply
define an
:raw-latex:`\linkResourceDirective{Sd}{Device}{Archive Device}` to be a
directory. The default directory to store backups on disk is
:raw-latex:`\path`\|/var/lib/bareos/storage\|:



::

    Device {
      Name = FileBackup
      Media Type = File
      Archive Device = /var/lib/bareos/storage
      Random Access = Yes;
      AutomaticMount = yes;
      RemovableMedia = no;
      AlwaysOpen = no;
    }



Assuming you have the appropriate :raw-latex:`\configresource{Storage}`
resource in your Director’s configuration file that references the above
Device resource,



::

    Storage {
      Name = FileStorage
      Address = ...
      Password = ...
      Device = FileBackup
      Media Type = File
    }



Bareos will then write the archive to the file
**/var/lib/bareos/storage/<volume-name>** where <volume-name> is the
volume name of a Volume defined in the Pool. For example, if you have
labeled a Volume named **Vol001**, Bareos will write to the file
**/var/lib/bareos/storage/Vol001**. Although you can later move the
archive file to another directory, you should not rename it or it will
become unreadable by Bareos. This is because each archive has the
filename as part of the internal label, and the internal label must
agree with the system filename before Bareos will use it.

Although this is quite simple, there are a number of problems. The first
is that unless you specify otherwise, Bareos will always write to the
same volume until you run out of disk space. This problem is addressed
below.

In addition, if you want to use concurrent jobs that write to several
different volumes at the same time, you will need to understand a number
of other details. An example of such a configuration is given at the end
of this chapter under :ref:`ConcurrentDiskJobs`.

Pool Options to Limit the Volume Usage
--------------------------------------


.. index:: 
   triple: General; Pool; Options to Limit the Volume Usage

Some of the options you have, all of which are specified in the Pool
record, are:

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volume Jobs}`:
   write only the specified number of jobs on each Volume.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volume Bytes}`:
   limit the maximum size of each Volume.

   Note, if you use disk volumes you should probably limit the Volume
   size to some reasonable value. If you ever have a partial hard disk
   failure, you are more likely to be able to recover more data if they
   are in smaller Volumes.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Use Duration}`:
   restrict the time between first and last data written to Volume.

Note that although you probably would not want to limit the number of
bytes on a tape as you would on a disk Volume, the other options can be
very useful in limiting the time Bareos will use a particular Volume (be
it tape or disk). For example, the above directives can allow you to
ensure that you rotate through a set of daily Volumes if you wish.

As mentioned above, each of those directives is specified in the Pool or
Pools that you use for your Volumes. In the case of
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volume Jobs}`,
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volume Bytes}` and
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Use Duration}`, you
can actually specify the desired value on a Volume by Volume basis. The
value specified in the Pool record becomes the default when labeling new
Volumes. Once a Volume has been created, it gets its own copy of the
Pool defaults, and subsequently changing the Pool will have no effect on
existing Volumes. You can either manually change the Volume values, or
refresh them from the Pool defaults using the
:command:`update volume` command in the Console. As an
example of the use of one of the above, suppose your Pool resource
contains:

.. raw:: latex

   \begin{bconfig}{Volume Use Duration}
   Pool {
     Name = File
     Pool Type = Backup
     Volume Use Duration = 23h
   }
   \end{bconfig}

then if you run a backup once a day (every 24 hours), Bareos will use a
new Volume for each backup, because each Volume it writes can only be
used for 23 hours after the first write. Note, setting the use duration
to 23 hours is not a very good solution for tapes unless you have
someone on-site during the weekends, because Bareos will want a new
Volume and no one will be present to mount it, so no weekend backups
will be done until Monday morning.

Automatic Volume Labeling
-------------------------


.. index:: 
   triple: General; Label; Automatic Volume Labeling

.. index:: 
   triple: General; Volume!Labeling; Automatic

Use of the above records brings up another problem – that of labeling
your Volumes. For automated disk backup, you can either manually label
each of your Volumes, or you can have Bareos automatically label new
Volumes when they are needed.

Please note that automatic Volume labeling can also be used with tapes,
but it is not nearly so practical since the tapes must be pre-mounted.
This requires some user interaction. Automatic labeling from templates
does NOT work with autochangers since Bareos will not access unknown
slots. There are several methods of labeling all volumes in an
autochanger magazine. For more information on this, please see the
:ref:`AutochangersChapter` chapter.

Automatic Volume labeling is enabled by making a change to both the
:raw-latex:`\resourcetype{Dir}{Pool}` resource and to the
:raw-latex:`\resourcetype{Sd}{Device}` resource shown above. In the case
of the Pool resource, you must provide Bareos with a label format that
it will use to create new names. In the simplest form, the label format
is simply the Volume name, to which Bareos will append a four digit
number. This number starts at 0001 and is incremented for each Volume
the catalog contains. Thus if you modify your Pool resource to be:

.. raw:: latex

   \begin{bconfig}{Label Format}
   Pool {
     Name = File
     Pool Type = Backup
     Volume Use Duration = 23h
     Label Format = "Vol"
   }
   \end{bconfig}

Bareos will create Volume names Vol0001, Vol0002, and so on when new
Volumes are needed. Much more complex and elaborate labels can be
created using variable expansion defined in the
:ref:`Variable Expansion VarsChapter` chapter of this
manual.

The second change that is necessary to make automatic labeling work is
to give the Storage daemon permission to automatically label Volumes. Do
so by adding
:raw-latex:`\linkResourceDirective{Sd}{Device}{Label Media}` = yes to
the :raw-latex:`\configresource{Device}` resource as follows:

.. raw:: latex

   \begin{bconfig}{Label Media = yes}
   Device {
     Name = File
     Media Type = File
     Archive Device = /var/lib/bareos/storage/
     Random Access = yes
     Automatic Mount = yes
     Removable Media = no
     Always Open = no
     Label Media = yes
   }
   \end{bconfig}

See :raw-latex:`\linkResourceDirective{Dir}{Pool}{Label Format}` for
details about the labeling format.

Restricting the Number of Volumes and Recycling
-----------------------------------------------


.. index:: 
   triple: General; Recycling; Restricting the Number of Volumes and Recycling
.. index:: General; Restricting the Number of Volumes and Recycling 

Automatic labeling discussed above brings up the problem of Volume
management. With the above scheme, a new Volume will be created every
day. If you have not specified Retention periods, your Catalog will
continue to fill keeping track of all the files Bareos has backed up,
and this procedure will create one new archive file (Volume) every day.

The tools Bareos gives you to help automatically manage these problems
are the following:

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{File Retention}`:
   catalog file record retention period.

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Job Retention}`:
   catalog job record retention period.

-  :raw-latex:`\linkResourceDirective{Dir}{Client}{Auto Prune}` = yes:
   permit the application of the above two retention periods.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Retention}`

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Auto Prune}` = yes:
   permit the application of the
   :raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Retention}`
   period.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Recycle}` = yes: permit
   automatic recycling of Volumes whose Volume retention period has
   expired.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Recycle Oldest Volume}`
   = yes: prune the oldest volume in the Pool, and if all files were
   pruned, recycle this volume and use it.

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Recycle Current Volume}`
   = yes: prune the currently mounted volume in the Pool, and if all
   files were pruned, recycle this volume and use it.

-  | :raw-latex:`\linkResourceDirective{Dir}{Pool}{Purge Oldest Volume}`
     = yes: permits a forced recycling of the oldest Volume when a new
     one is needed.
   | :raw-latex:`\warning{This record ignores retention periods! We highly
        recommend  not to use this record, but instead use \linkResourceDirective{Dir}{Pool}{Recycle Oldest Volume}.}`

-  :raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volumes}`:
   limitthe number of Volumes that can be created.

The first three records
(:raw-latex:`\linkResourceDirective{Dir}{Client}{File Retention}`,
:raw-latex:`\linkResourceDirective{Dir}{Client}{Job Retention}` and
:raw-latex:`\linkResourceDirective{Dir}{Client}{Auto Prune}`) determine
the amount of time that Job and File records will remain in your Catalog
and they are discussed in detail in the
:ref:`Automatic Volume Recycling RecyclingChapter`
chapter.

:raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Retention}`,
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Auto Prune}` and
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Recycle}` determine how
long Bareos will keep your Volumes before reusing them and they are also
discussed in detail in the
:ref:`Automatic Volume Recycling RecyclingChapter`
chapter.

The :raw-latex:`\linkResourceDirective{Dir}{Pool}{Maximum Volumes}`
record can also be used in conjunction with the
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Retention}` period
to limit the total number of archive Volumes that Bareos will create. By
setting an appropriate
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Volume Retention}` period,
a Volume will be purged just before it is needed and thus Bareos can
cycle through a fixed set of Volumes. Cycling through a fixed set of
Volumes can also be done by setting
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Purge Oldest Volume}` =
yes or
:raw-latex:`\linkResourceDirective{Dir}{Pool}{Recycle Current Volume}` =
yes. In this case, when Bareos needs a new Volume, it will prune the
specified volume.

Concurrent Disk Jobs
====================

.. index:: General; Concurrent Disk Jobs 
.. _ConcurrentDiskJobs: Above, we discussed how you
could have a single device named
:raw-latex:`\resourcename{Sd}{Device}{FileBackup}` that writes to
volumes in */var/lib/bareos/storage/*. You can, in fact, run multiple
concurrent jobs using the Storage definition given with this example,
and all the jobs will simultaneously write into the Volume that is being
written.

Now suppose you want to use multiple Pools, which means multiple
Volumes, or suppose you want each client to have its own Volume and
perhaps its own directory such as **/home/bareos/client1** and
**/home/bareos/client2** ... . With the single Storage and Device
definition above, neither of these two is possible. Why? Because Bareos
disk storage follows the same rules as tape devices. Only one Volume can
be mounted on any Device at any time. If you want to simultaneously
write multiple Volumes, you will need multiple Device resources in your
 |bareosSd| configuration and thus multiple Storage resources
in your  |bareosDir| configuration.

Okay, so now you should understand that you need multiple Device
definitions in the case of different directories or different Pools, but
you also need to know that the catalog data that Bareos keeps contains
only the Media Type and not the specific storage device. This permits a
tape for example to be re-read on any compatible tape drive. The
compatibility being determined by the Media Type
(:raw-latex:`\linkResourceDirective{Dir}{Storage}{Media Type}` and
:raw-latex:`\linkResourceDirective{Sd}{Device}{Media Type}`). The same
applies to disk storage. Since a volume that is written by a Device in
say directory :raw-latex:`\path`\|/home/bareos/backups\| cannot be read
by a Device with an
:raw-latex:`\linkResourceDirective{Sd}{Device}{Archive Device}` =
:raw-latex:`\path`\|/home/bareos/client1\|, you will not be able to
restore all your files if you give both those devices
:raw-latex:`\linkResourceDirective{Sd}{Device}{Media Type}` = File.
During the restore, Bareos will simply choose the first available
device, which may not be the correct one. If this is confusing, just
remember that the Directory has only the Media Type and the Volume name.
It does not know the
:raw-latex:`\linkResourceDirective{Sd}{Device}{Archive Device}` (or the
full path) that is specified in the  |bareosSd| . Thus you
must explicitly tie your Volumes to the correct Device by using the
Media Type.

Example for two clients, separate devices and recycling
-------------------------------------------------------

The following example is not very practical, but can be used to
demonstrate the proof of concept in a relatively short period of time.

The example consists of a two clients that are backed up to a set of 12
Volumes for each client into different directories on the Storage
machine. Each Volume is used (written) only once, and there are four
Full saves done every hour (so the whole thing cycles around after three
hours).

What is key here is that each physical device on the
 |bareosSd| has a different Media Type. This allows the
Director to choose the correct device for restores.

The  |bareosDir| configuration is as follows:

.. raw:: latex

   \begin{bconfig}{}
   Director {
     Name = bareos-dir
     QueryFile = "/usr/lib/bareos/scripts/query.sql"
     Password = "<secret>"
   }

   Schedule {
     Name = "FourPerHour"
     Run = Level=Full hourly at 0:05
     Run = Level=Full hourly at 0:20
     Run = Level=Full hourly at 0:35
     Run = Level=Full hourly at 0:50
   }

   FileSet {
     Name = "Example FileSet"
     Include {
       Options {
         compression=GZIP
         signature=SHA1
       }
       File = /etc
     }
   }

   Job {
     Name = "RecycleExample"
     Type = Backup
     Level = Full
     Client = client1-fd
     FileSet= "Example FileSet"
     Messages = Standard
     Storage = FileStorage
     Pool = Recycle
     Schedule = FourPerHour
   }

   Job {
     Name = "RecycleExample2"
     Type = Backup
     Level = Full
     Client = client2-fd
     FileSet= "Example FileSet"
     Messages = Standard
     Storage = FileStorage2
     Pool = Recycle2
     Schedule = FourPerHour
   }

   Client {
     Name = client1-fd
     Address = client1.example.com
     Password = client1_password
   }

   Client {
     Name = client2-fd
     Address = client2.example.com
     Password = client2_password
   }

   Storage {
     Name = FileStorage
     Address = bareos-sd.example.com
     Password = local_storage_password
     Device = RecycleDir
     Media Type = File
   }

   Storage {
     Name = FileStorage2
     Address = bareos-sd.example.com
     Password = local_storage_password
     Device = RecycleDir2
     Media Type = File1
   }

   Catalog {
     Name = MyCatalog
     ...
   }

   Messages {
     Name = Standard
     ...
   }

   Pool {
     Name = Recycle
     Pool Type = Backup
     Label Format = "Recycle-"
     Auto Prune = yes
     Use Volume Once = yes
     Volume Retention = 2h
     Maximum Volumes = 12
     Recycle = yes
   }

   Pool {
     Name = Recycle2
     Pool Type = Backup
     Label Format = "Recycle2-"
     Auto Prune = yes
     Use Volume Once = yes
     Volume Retention = 2h
     Maximum Volumes = 12
     Recycle = yes
   }
   \end{bconfig}

and the  |bareosSd| configuration is:

.. raw:: latex

   \begin{bconfig}{}
   Storage {
     Name = bareos-sd
     Maximum Concurrent Jobs = 10
   }

   Director {
     Name = bareos-dir
     Password = local_storage_password
   }

   Device {
     Name = RecycleDir
     Media Type = File
     Archive Device = /home/bareos/backups
     LabelMedia = yes;
     Random Access = Yes;
     AutomaticMount = yes;
     RemovableMedia = no;
     AlwaysOpen = no;
   }

   Device {
     Name = RecycleDir2
     Media Type = File2
     Archive Device = /home/bareos/backups2
     LabelMedia = yes;
     Random Access = Yes;
     AutomaticMount = yes;
     RemovableMedia = no;
     AlwaysOpen = no;
   }

   Messages {
     Name = Standard
     director = bareos-dir = all
   }
   \end{bconfig}

With a little bit of work, you can change the above example into a
weekly or monthly cycle (take care about the amount of archive disk
space used).

Using Multiple Storage Devices
------------------------------

.. index:: General; Multiple Storage Devices 

.. index:: 
   triple: General; Storage Device; Multiple

Bareos treats disk volumes similar to tape volumes as much as it can.
This means that you can only have a single Volume mounted at one time on
a disk as defined in your :raw-latex:`\resourcetype{Sd}{Device}`
resource.

If you use Bareos without :ref:`sec:DataSpooling`,
multiple concurrent backup jobs can be written to a Volume using
interleaving. However, interleaving has disadvantages, see
:ref:`sec:Interleaving`.

Also the :raw-latex:`\resourcetype{Sd}{Device}` will be in use. If there
are other jobs, requesting other Volumes, these jobs have to wait.

On a tape (or autochanger), this is a physical limitation of the
hardware. However, when using disk storage, this is only a limitation of
the software.

To enable Bareos to run concurrent jobs (on disk storage), define as
many :raw-latex:`\resourcetype{Sd}{Device}` as concurrent jobs should
run. All these :raw-latex:`\resourcetype{Sd}{Device}`s can use the same
:raw-latex:`\linkResourceDirective{Sd}{Device}{Archive Device}`
directory. Set
:raw-latex:`\linkResourceDirective{Sd}{Device}{Maximum Concurrent Jobs}`
= 1 for all these devices.

Example: use four storage devices pointing to the same directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: latex

   \begin{bconfig}{\bareosDir configuration: using 4 storage devices}
   Director {
     Name = bareos-dir.example.com
     QueryFile = "/usr/lib/bareos/scripts/query.sql"
     Maximum Concurrent Jobs = 10
     Password = "<secret>"
   }

   Storage {
     Name = File
     Address = bareos-sd.bareos.com
     Password = "<sd-secret>"
     Device = FileStorage1
     Device = FileStorage2
     Device = FileStorage3
     Device = FileStorage4
     # number of devices = Maximum Concurrent Jobs
     Maximum Concurrent Jobs = 4
     Media Type = File
   }

   [...]
   \end{bconfig}

.. raw:: latex

   \begin{bconfig}{\bareosSd configuraton: using 4 storage devices}
   Storage {
     Name = bareos-sd.example.com
     # any number >= 4
     Maximum Concurrent Jobs = 20
   }

   Director {
     Name = bareos-dir.example.com
     Password = "<sd-secret>"
   }

   Device {
     Name = FileStorage1
     Media Type = File
     Archive Device = /var/lib/bareos/storage
     LabelMedia = yes
     Random Access = yes
     AutomaticMount = yes
     RemovableMedia = no
     AlwaysOpen = no
     Maximum Concurrent Jobs = 1
   }

   Device {
     Name = FileStorage2
     Media Type = File
     Archive Device = /var/lib/bareos/storage
     LabelMedia = yes
     Random Access = yes
     AutomaticMount = yes
     RemovableMedia = no
     AlwaysOpen = no
     Maximum Concurrent Jobs = 1
   }

   Device {
     Name = FileStorage3
     Media Type = File
     Archive Device = /var/lib/bareos/storage
     LabelMedia = yes
     Random Access = yes
     AutomaticMount = yes
     RemovableMedia = no
     AlwaysOpen = no
     Maximum Concurrent Jobs = 1
   }

   Device {
     Name = FileStorage4
     Media Type = File
     Archive Device = /var/lib/bareos/storage
     LabelMedia = yes
     Random Access = yes
     AutomaticMount = yes
     RemovableMedia = no
     AlwaysOpen = no
     Maximum Concurrent Jobs = 1
   }
   \end{bconfig}
