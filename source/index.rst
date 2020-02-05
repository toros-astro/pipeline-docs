.. TOROS Pipeline Documentation documentation master file, created by
   sphinx-quickstart on Wed Feb  5 12:57:37 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. toctree::
   :hidden:

   installation
   requirements
   modules

The TOROS Science Pipeline
==========================

TOROS goal is to enable optical follow-up to gravitational wave alerts
issued by the `LIGO/Virgo Public Alerts <https://emfollow.docs.ligo.org/>`_.

This document describes the TOROS pipeline structure
that will control the adquisition and processing of the image data.
It is intended for users and developers for the TOROS pipeline.

Pipeline Basic Diagram
----------------------

When an alert is issued by the LVC, the lvcgcn daemon will receive the alert,
in the form of a VOEvent, process its contents and generate a list of potential
host galaxies. The information is then relayed to the observatories.
For a more detailed description of the lvcgcn receiver,
please see `lvcgcn <https://lvcgcn.readthedocs.io>`_. 
