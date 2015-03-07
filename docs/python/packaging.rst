Packaging Python modules
========================

The `Python Packaging User Guide`_ has excellent guidance on packaging Python projects - in particular, use the information on `packaging and distributing projects <distributing projects_>`_, and the `suggested tools`_. Python `projects <project_>`_ that provide a package_ should include :file:`setup.py` and :file:`setup.cfg` configuration files:

.. literalinclude:: examples/setup.py
    :language: python

Notes on specific metadata items:

- Version numbers should follow the `semantic versioning specification`_.
- PyPI_ provides `a list of available package classifiers <classifiers_>`_.
  - Python 3 only projects should use ``Programming Language :: Python :: 3 :: Only``.
- Python projects should use the MIT License (see :doc:`/projects/index`).

Packages that run on Python 2 and 3 should ensure they have a :file:`setup.cfg` file that configures ``bdist_wheel`` to mark the wheel as 'universal' (otherwise, the wheel will declare that it is only for the version of Python it was built on).

.. literalinclude:: examples/setup.cfg
    :language: ini

PyPi
----

A new python package can be registered to PyPI_ with:

.. code-block:: bash

    python setup.py register

Python packages can generally be released with:

.. code-block:: bash

    python setup.py sdist bdist_wheel upload

Tox can be used to automate package releases, by including a test environment that runs the release commands:

.. literalinclude:: examples/tox.ini
    :language: ini
    :start-after: sphinx_rtd_theme

In the unusual case that a package supplies metadata depending on which Python version it is running on (see complex_setup_example_), you'll need to run `bdist_wheel` for each of those Python versions. While source distributions run `setup.py` when *installing* a package, built distributions run `setup.py` when creating the package).

.. code-block:: ini

    [testenv:release]
    commands=
        python2 setup.py sdist upload
        python2 setup.py bdist_wheel upload
        python3 setup.py bdist_wheel upload
    deps=wheel

.. |complex_setup_example| replace:: ``riemann-client/setup.py``
.. _complex_setup_example: https://github.com/borntyping/python-riemann-client/blob/master/setup.py

Readme
------

README files for Python projects should use Markdown_ (see `this commit <https://github.com/borntyping/tg/commit/98e0215da6948ddf038d39cbea00c708c94475a1>`_). The README should include links to the GitHub_ repository, any packages on PyPi_,builds on `Travis-CI`_ and documentation on `Read The Docs`_ (which is especially useful when the README is shown in multiple places).

.. literalinclude:: examples/README.md
    :language: markdown

You will need to create a ``MANIFEST.in`` file so that the README is included in the package:

.. literalinclude:: examples/MANIFEST.in`

README files for older Python projects using reStructuredText_ can use the `rst-lint`_ tool for checking the validity of a README file.

.. literalinclude:: examples/README.rst
    :language: reStructuredText

.. _Python Packaging User Guide: https://packaging.python.org/en/latest/
.. _distributing projects: https://packaging.python.org/en/latest/distributing.html
.. _suggested tools: https://packaging.python.org/en/latest/current.html
.. _project: https://packaging.python.org/en/latest/glossary.html#term-project
.. _package: https://packaging.python.org/en/latest/glossary.html#term-import-package
.. _classifiers: https://pypi.python.org/pypi?%3Aaction=list_classifiers
.. _rst-lint: https://pypi.python.org/pypi/restructuredtext_lint
.. _PyPI: https://pypi.python.org/pypi/
.. _warehouse: https://warehouse.python.org/
.. _Travis-CI: https://travis-ci.org/
.. _Read The Docs: https://readthedocs.org/
.. _GitHub:  https://github.com/

.. HTTPS not availible for these links
.. _semantic versioning specification: http://semver.org/spec/v2.0.0.html
.. _reStructuredText: https://docutils.sourceforge.net/rst.html
.. _Markdown: http://commonmark.org/
