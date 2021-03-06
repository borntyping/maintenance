Packaging checklist
===================

Creating a new package
----------------------

Package metadata
    Create ``setup.py`` and ``setup.cfg``

Testing metadata
    Create ``tox.ini`` and ``travis.yml``

Package registration
    ``python setup.py register``

Releasing a package
-------------------

Run tests
    ``tox``

Update metadata
    Update version numbers in ``setup.py`` and ``__init__.py``

Tag release
    |git-tag-version|_ *or* ``git tag -a "v0.1.0" -m "Version 0.1.0"``

Package upload
    ``tox -e release`` or ``python setup.py sdist bdist_wheel upload``

Documenation
------------

Build Sphinx documenation
    ``sphinx-build docs docs/_build``

Open Sphinx documenation
    ``xdg-open docs/_build/index.html``

.. include:: ../references.rst
