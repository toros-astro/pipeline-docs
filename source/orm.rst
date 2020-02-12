.. _orm:

.. warning::
  This is work in progress and may change in the future.

Database Schema
===============

**Exposure**: A single CCD raw exposure.
 
 Examples:

- Flat fields
- Dark frames
- Light exposures

 Attributes:

- exposure_type
- exposure_time
- npix1
- npix2
- ...

**Combination**: Any type of combination of files.

Examples:

- A median-stack of exposures.
- A difference image of source and reference.
- A stack of calibration files, like a dark stack.

Attributes:

- combination_type
- ...

**FileBatch**: A set of related Exposures.

Examples:

- Dark, Flat and Light exposures of a single night.

Attributes:

- Many-to-many relation with Exposure
- Calibration Status (foreign key relation)

**Status Codes**: The status code (error or success) for different processes.

Example:

- 0 may mean success.
- 100-199 Error codes may refer to codes during calibration.

Attributes:

- number_code
- description
