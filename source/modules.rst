.. _modules:

Modules
=======

Telescope
---------

Public API: TBD

Machine finishes taking images for a specific request or routine imaging.

Notify Processor machine that there are new raw exposures in some folder.
The collection of these calibration and light frames will be referred from now on as a *file batch*.

Processor
---------

The process begins when the work order is received by the Telescope module 
or any other external request.

- Processor machine transfers file batch to local repo (if necessary).
- Processor begins sequence of steps to calibrate (preprocess, reduce) the images.
- Specific steps are flat stacking, dark stacking, flat-dark correction, astrometry, etc.

Example of a single step
^^^^^^^^^^^^^^^^^^^^^^^^

Let's suppose we want to do a Dark stacking.

- Query the database for all ``Exposure`` of type ``dark`` in given ``FileBatch``.
- Group the ``Exposure`` by exposure time ``exptime`` and ``filter`` if any.
- Make one stack per group and save to file.
- Create an entry for each dark stack in the database.
- If no errors
    - Record in the database that process was completed with no errors.
    - Return control.
- If there were errors
    - Record in the database an error.
    - Raise an Exception.
    - The caller function should catch the exception and log the error
      (this should trigger an email send to all admins).
    - The caller function can either return control
      or skip the step and continue with the next step.


.. _wo:

Work Orders
-----------

An example of a work order sent to the Preprocessor::

  work_order = {
      "id": "1",
      "request": "calibrate_file_batch",
      "url": https://myaddres.org/get?allfiles,
      "datetime": "2019-03-05T14:34:54.234",
      "user": "Main Module",
      ...
  }

``request`` could be one of the following: ``calibrate_file_batch``, ``resume_file_batch``, ``restart_file_batch``, etc.

Here is an example of a work order sent to telescope::

  work_order = {
      "id": "1",
      "request": "observation",
      "priority": None,
      "datetime": "2019-03-05T14:34:54.234",
      "ra" = 132.23356,
      "dec" = 34.254534,
      "user": "Main Module",
      ...
  }

``priority`` is assigned by the scheduler in the Telescope module when receiving the WO.
It will be a float number in the range 0-10.
