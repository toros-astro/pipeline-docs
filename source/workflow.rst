Pipeline Workflow
=================

Modules
-------

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

Automatic target scheduling.
Dome and telescope operated manually, possibly remotely.
Calibration of files done automatically but triggered manually at the end of the night.

Stage 2
^^^^^^^

Dome and telescope operated remotely with scripts.
Explore Linux-based telescope operation.
Windows-Linux connection for communication.

Stage 3
^^^^^^^

Dome and telescope synchronized.
Calibration of files triggered by telescope.
Web interface to interact with telescope and processor.
