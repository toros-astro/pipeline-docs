[![Build Status](https://travis-ci.org/toros-astro/pipeline-docs.svg?branch=master)](https://travis-ci.org/toros-astro/pipeline-docs)

# The TOROS Science Pipeline Documentation

TOROS goal is to enable optical follow-up to gravitational wave alerts
issued by the [LIGO/Virgo Public Alerts](https://emfollow.docs.ligo.org).

This repository contains the files that are compiled and hosted
on the official [TOROS pipeline website](https://toros.utrgv.edu/pipeline).

### Compilation

The documentation is created using [Sphinx](https://www.sphinx-doc.org).
And uses the [Sphinx RTD theme](https://sphinx-rtd-theme.readthedocs.io).

To compile locally, install the dependencies and make the html pages:

    $ pip install sphinx sphinx_rtd_theme
    $ make html

The html output should be in `build/html/index.html`.

***

(c) 2020, TOROS Dev Team.
