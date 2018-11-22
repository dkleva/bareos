Catalog Tables
==============

.. index:: General; Catalog 

Bareos stores its information in a database, named Catalog. It is
configured by :ref:`DirectorResourceCatalog`.

Job
---


.. index:: 
   triple: General; Catalog; Job

.. index:: 
   triple: General; Job; Catalog

JobStatus
~~~~~~~~~


.. index:: 
   triple: General; Job; JobStatus

.. index:: 
   triple: General; Catalog!Job; JobStatus

The status of a Bareos job is stored as abbreviation in the Catalog
database table Job. It is also displayed by some bconsole commands, eg.
:command:`list jobs`.

This table lists the abbreviations together with its description and
weight. The weight is used, when multiple states are applicable for a
job. In this case, only the status with the highest weight/priority is
applied.

+-----------------------+-----------------------+-----------------------+
| **Abbr.**             | :raw-latex:`\multicol | **Weight**            |
|                       | umn{1}{c|}{\textbf{De |                       |
|                       | scription}}`          |                       |
+=======================+=======================+=======================+
| C                     | Created, not yet      | 15                    |
|                       | running               |                       |
+-----------------------+-----------------------+-----------------------+
| R                     | Running               | 15                    |
+-----------------------+-----------------------+-----------------------+
| B                     | Blocked               | 15                    |
+-----------------------+-----------------------+-----------------------+
| T                     | Completed             | 10                    |
|                       | successfully          |                       |
+-----------------------+-----------------------+-----------------------+
| E                     | Terminated with       | 25                    |
|                       | errors                |                       |
+-----------------------+-----------------------+-----------------------+
| e                     | Non-fatal error       | 20                    |
+-----------------------+-----------------------+-----------------------+
| f                     | Fatal error           | 100                   |
+-----------------------+-----------------------+-----------------------+
| D                     | Verify found          | 15                    |
|                       | differences           |                       |
+-----------------------+-----------------------+-----------------------+
| A                     | Canceled by user      | 90                    |
+-----------------------+-----------------------+-----------------------+
| I                     | Incomplete job        | 15                    |
+-----------------------+-----------------------+-----------------------+
| L                     | Committing data       | 15                    |
+-----------------------+-----------------------+-----------------------+
| W                     | Terminated with       | 20                    |
|                       | warnings              |                       |
+-----------------------+-----------------------+-----------------------+
| l                     | Doing data despooling | 15                    |
+-----------------------+-----------------------+-----------------------+
| q                     | Queued waiting for    | 15                    |
|                       | device                |                       |
+-----------------------+-----------------------+-----------------------+
| F                     | Waiting for Client    | 15                    |
+-----------------------+-----------------------+-----------------------+
| S                     | Waiting for Storage   | 15                    |
|                       | daemon                |                       |
+-----------------------+-----------------------+-----------------------+
| m                     | Waiting for new media | 15                    |
+-----------------------+-----------------------+-----------------------+
| M                     | Waiting for media     | 15                    |
|                       | mount                 |                       |
+-----------------------+-----------------------+-----------------------+
| s                     | Waiting for storage   | 15                    |
|                       | resource              |                       |
+-----------------------+-----------------------+-----------------------+
| j                     | Waiting for job       | 15                    |
|                       | resource              |                       |
+-----------------------+-----------------------+-----------------------+
| c                     | Waiting for client    | 15                    |
|                       | resource              |                       |
+-----------------------+-----------------------+-----------------------+
| d                     | Waiting on maximum    | 15                    |
|                       | jobs                  |                       |
+-----------------------+-----------------------+-----------------------+
| t                     | Waiting on start time | 15                    |
+-----------------------+-----------------------+-----------------------+
| p                     | Waiting on higher     | 15                    |
|                       | priority jobs         |                       |
+-----------------------+-----------------------+-----------------------+
| i                     | Doing batch insert    | 15                    |
|                       | file records          |                       |
+-----------------------+-----------------------+-----------------------+
| a                     | SD despooling         | 15                    |
|                       | attributes            |                       |
+-----------------------+-----------------------+-----------------------+
