.. _req:

Requirements
============

Software
--------

The modules will run as services (background daemons)
on the same machine or in different machines connected by the same network.

Modules will retrieve file input (typically FITS images) information from
the database.

When the operation is completed, the module should also write to the database
the information of the new files generated.

The pipeline should have a way to resume processing on failed targets,
either from command line or via XML-RPC request.

The modules should have a command line API
as well as a public API exposed via XML-RPC or other protocol.

Logging
-------

Logging to a file and cycled (archived) daily.

Logging level should be ``DEBUG`` initially and later changed to ``ERROR``.

When logging ``ERROR``, they should also be emailed to the ``ADMIN`` list in the configuration file.

Network
-------

Modules must be able to communicate either

* Locally using ports;
* Remotely to a computer in the same network;
* Over Internet using HTTP or other protocol

Modules should have read-write access to the database.

Hardware
--------

No requirements.

FITS HEADERS
------------

TBD

Database
--------

Postgresql or SQLite for development.

ORM: TBD

Schema: TBD

Error Code & Status: TBD
