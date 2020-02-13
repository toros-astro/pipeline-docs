Overview
========

Modules
-------

Each TOROS module will run as a daemon (background process)
and work on a specific port specified in the configuration file using the XML-RPC (or HTTP) protocol.

Each service responds to a single function called ``front_desk`` which accepts a "Work Order".
Work Orders (WO) are dictionaries with a specific structure described (see section :ref:`wo`).

The specific editable parameters taken by the modules, like the database name,
the port for each service, etc, are set on a global configuration file (one per network node).
Each module loads and keeps a copy of the configuration parameters at loading time.
If configuration parameters are changed, all the modules have to be restarted.
See :ref:`conf`.

Next, we describe 3 modules of the pipeline. More can be added in the future.
See :ref:`modules` for a full description.

Alert Robot (lvcgcn)
^^^^^^^^^^^^^^^^^^^^

When an alert is issued by the LVC, the lvcgcn daemon will receive the alert,
in the form of a VOEvent, process its contents and generate a list of potential
host galaxies. The information is then relayed to the observatories.
For a more detailed description of the lvcgcn receiver,
please see `lvcgcn <https://lvcgcn.readthedocs.io>`_. 

Telescope
^^^^^^^^^

The telescope module is a background process running continuously and listening
for requests on a designated port.
Communication protocol could be HTTP, TCP/IP or XML-RPC.

Telescope can receive requests from 
  
Tasks:
  
- Control dome.
- Receive targets from alert.
- Schedule (order) targets before night.
- Point telescope.
- Take images.
- Take calibration frames (flat, dark).
- Prepare for night.
- Close night.
- Open night.
- Store images.
- Notify other modules.

Preprocessor
^^^^^^^^^^^^

Full documentation in the `torosmanager <https://torosmanager.readthedocs.io>`_
webpage.

The preprocessor module is a background process running continuously and listening
for requests on a designated port.
Communication protocol could be HTTP, TCP/IP or XML-RPC.

The preprocessor module is in charge of calibrating the CCD exposures after an observation night.

It may also be in charge of further analysis like optical transient (OT) detection,
or that could be managed by a separate analysis pipeline.

Preprocessor can receive requests from telescope module and other external requests.
This could come from the local machine through command line scripts or remotely
through a web interface or remote scripts.

Typically, it will be telescope notifying the preprocessor that a batch of files
is ready and request a calibration.

Data Products
-------------

* Calibrated Images
* Other TBD (Catalogs? OT Reports?)

Development Stages
------------------

The Development will be divided into (roughly) 3 stages of progressive autonomy:

Stage 1
^^^^^^^

- Automatic target scheduling.
- Dome and telescope operated manually, possibly remotely.
- Calibration of files done automatically but triggered manually at the end of the night.
- Single execution thread for processes.

Stage 2
^^^^^^^

- Dome and telescope operated remotely with scripts.
- Explore Linux-based telescope operation.
- Windows-Linux connection for communication.
- Requests processed in separate threads.

Stage 3
^^^^^^^

- Dome and telescope synchronized.
- Calibration of files triggered by telescope.
- Web interface to interact with telescope and processor.

.. _conf:

Configuration file
------------------

A `YAML`_ configuration file for all services.
It is copied into ``/etc/toros/toros.conf.yaml`` at installation time.
It is meant to be edited after install.

Some parameters to change:

Preprocessor Service Address
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**HTTP:** The full address and port to locate the preprocessor service on the net.
Ex: ``http://127.168.0.1:8080``.

**IP:** The IP address of the server running the preprocessor service.
Ex: ``127.168.0.1``.

**Port:** The port for the address of the server running the preprocessor service.
Ex: ``8080``.

Logging
^^^^^^^

**File:** File path to the log file that will be used to log. Default is ``/etc/toros/logs/toros.log``.

**Log Level:** One of ``DEBUG``, ``INFO``, ``WARNING``, ``ERROR``. Default: ``INFO``.

Database
^^^^^^^^

Path and credentials to access the database.

.. _YAML: https://yaml.org