Development environments
========================

When installing packages for Python, Ruby or other similar languages, always avoid installing packages alongside packages installed with the systems package manager.

Python
------

Use pipsi_ to install python tools, and virtualenv_/tox_ to install project dependencies. If it's necessary to install packages into a global namespace, use ``pip install --user``. v_ and virtualenvwrapper_ are useful tools to manage a set of Python virtual environments.

Python 2.7 is a required package on Debian and RHEL systems, and often comes with python modules installed via the system's package manager. **It's a really bad idea to install python packages that aren't managed by the system package manager into the system's Python installation.** In particular, pip_ may break things on some versions of Debian/Ubuntu due to the way the Debian packages are distributed.

.. _pip: http://pip.readthedocs.org/en/stable/
.. _pipsi: https://github.com/mitsuhiko/pipsi
.. _tox: http://tox.readthedocs.org/
.. _virtualenv: https://virtualenv.pypa.io/en/latest/
.. _virtualenvwrapper: http://virtualenvwrapper.readthedocs.org/en/latest/
.. _v: https://github.com/borntyping/v/

Ruby
----

Use ``gem install --user-install`` to install gems into your home directory instead of the systems folders. rvm_ can be used to install and manage multiple Ruby versions. bundler_ can be used to manage project dependencies.

Uninstall **all** Ruby gems with:

.. code-block:: bash

    gem list | cut -d" " -f1 | xargs sudo gem uninstall -aIx

.. _rvm: https://rvm.io/
.. _bundler: http://bundler.io/
