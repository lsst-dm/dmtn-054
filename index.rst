..
  Technote content.

  See https://developer.lsst.io/docs/rst_styleguide.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. Add content below. Do not include the document title.

.. note::

   **This technote is not yet published.**

The `LSST verify framework <https://github.com/lsst/verify>`_ involves the creation of Measurements throughout the Stack. These Measurements must be delivered to the `ap_verify framework <https://github.com/lsst-dm/ap_verify>`_ so that it can manage them and forward them to SQuaSH. We would like to integrate the ``verify`` code into the Stack in a way that minimizes the knowledge ``ap_verify`` must have of pipeline implementation details and maximizes the maintainability of the individual Tasks that will be instrumented. This document describes the conventions the ``ap_verify`` team has adopted to achieve both goals.

Metric definitions
==================

All AP verification metrics shall be stored in the `verify_metrics <https://github.com/lsst/verify_metrics>`_ package, following that package's conventions. Metrics and conventions for describing them are described on `Confluence <https://confluence.lsstcorp.org/display/~ebellm/Alert+Production+Metrics>`_; in particular, all our metrics should be tagged ``ap_verify`` for easy filtering and identification.

Data Flow
=========

Each Task shall be responsible for the persistence of its own Measurements. As described in `SQR-019`_, this may be done by creating a Job object and attaching Measurements and Task-specific metadata, or through ``output_quantities``.

Each Task must write its Measurements to disk in a location that will persist to at least the end of the pipeline run, and store the absolute path to the file in a metadata key named "<standard task prefix>.verify_json_path". ``ap_verify`` shall read any Measurement files mentioned in a Task's metadata, including files associated with subTasks.

.. _SQR-019: https://sqr-019.lsst.io/

Instrumenting Tasks
===================

TBD

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :encoding: latex+latin
..    :style: lsst_aa
