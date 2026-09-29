.. _general:

Installation
=================================

1. ``pip install  --no-cache-dir django-multitenant-dt``

Supported Django and Citus versions/Pre-requisites
===================================================

======================== ====== =========
Python                   Django Citus
======================== ====== =========
3.12 3.13 3.14           6.0    13
3.10 3.11 3.12 3.13 3.14 5.2    13
3.10 3.11 3.12           4.2    13
======================== ====== =========

CI runs the test suite against plain PostgreSQL. Citus support was verified manually with Citus 13.
