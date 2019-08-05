.. _installing-packages:

===================
패키지 설치
===================

이 섹션에서는 파이썬 :term:`패키지 <Distribution Package>`\을 설치하는 방법에 대해 다룹니다.

이 문맥에서 "패키지"라는 용어는 :term:`배포 <Distribution Package>` (즉, 설치할 소프트웨어 
번들)의 동의어로 사용된다는 점을 유의해야합니다. 파이썬 코드 (즉, 모듈에서 컨테이너)에서 임포트하는
일종의 :term:`패키지 <Import Package>`\를 참조하지 않습니다. 파이썬 커뮤니티에서는 "패키지"라는 
용어를 사용하여 :term:`배포 <Distribution Package>`\를 나타냅니다. "배포"라는 용어를 사용하는 것은 
선호되지 않습니다. 리눅스 배포판과 혼동 될 수 있기 때문입니다. 배포 또는 파이썬과 같은 다른 큰 소프트웨어 
배포판을 포함할 수 있습니다.

.. contents:: Contents
   :local:


.. _installing_requirements:

패키지 설치 요구 사항
====================================

이 섹션에서는 다른 파이썬 패키지를 설치하기 전에 따라야 할 단계를 설명합니다.

커멘드 라인에서 파이썬을 실행할 수 있는지 확인
-----------------------------------------------

더 진행하기 전에, 파이썬을 설치되어있고, 커멘드 라인에서 예상되는 버전을 사용할 수 있는지 확인합니다. 
다음을 실행하여 이를 확인할 수 있습니다:

.. code-block:: bash

    python --version

``Python 3.6.3``\과 같은 결과가 출력되어야 합니다. 파이썬이 없다면, `python.org`_\에서 최신 
3.x 버전을 설치하거나 Hitchhiker's Guide to Python에서 `파이썬 설치`_ 세션을 참조하십시오.

.. Note:: 당신이 초보이고 다음과 같은 오류가 발생하면:

    .. code-block:: python

        >>> python --version
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
        NameError: name 'python' is not defined

    이 튜토리얼에서 이 명령과 다른 제안된 명령은 *shell* (*terminal* 또는 *console* 이라고도 함)
    에서 실행하기 위한 것입니다. 운영체제 셸 사용과 파이썬과의 상호작용에 대한 소개는 초보자를 위한 파이썬 
    시작하기 튜토리얼을 참조하십시오.

.. Note:: IPython이나 Jupyter 노트북과 같은 향상된 셸을 사용한다면, 이 튜토리얼에서와 같은 시스템 
   명령어 ``!`` 문자를 사용합니다:

    ::

        In [1]: import sys
                !{sys.executable} --version
        Python 3.6.3

   현재 실행중인 노트북에서 일치하는 파이썬 콘솔 명령어를 사용하려면 ``python``\이 아닌 
   ``{sys.executable}``\를 사용하는 것이 좋습니다. (``python`` 명령을 실행하는 것이 
   설치된 파이썬과 다를 수 있습니다.)

.. Note:: Due to the way most Linux distributions are handling the Python 3
   migration, Linux users using the system Python without creating a virtual
   environment first should replace the ``python`` command in this tutorial
   with ``python3`` and the ``pip`` command with ``pip3 --user``. Do *not*
   run any of the commands in this tutorial with ``sudo``: if you get a
   permissions error, come back to the section on creating virtual environments,
   set one up, and then continue with the tutorial as written.

.. _getting started tutorial: https://opentechschool.github.io/python-beginners/en/getting_started.html#what-is-python-exactly
.. _python.org: https://python.org

Ensure you can run pip from the command line
--------------------------------------------

Additionally, you'll need to make sure you have :ref:`pip` available. You can
check this by running:

.. code-block:: bash

    pip --version

If you installed Python from source, with an installer from `python.org`_, or
via `Homebrew`_ you should already have pip. If you're on Linux and installed
using your OS package manager, you may have to install pip separately, see
:doc:`/guides/installing-using-linux-tools`.

.. _Homebrew: https://brew.sh
.. _파이썬 설치: http://docs.python-guide.org/en/latest/starting/installation/

If ``pip`` isn't already installed, then first try to bootstrap it from the
standard library:

.. code-block:: bash

    python -m ensurepip --default-pip

If that still doesn't allow you to run ``pip``:

 * Securely Download `get-pip.py
   <https://bootstrap.pypa.io/get-pip.py>`_ [1]_

 * Run ``python get-pip.py``. [2]_  This will install or upgrade pip.
   Additionally, it will install :ref:`setuptools` and :ref:`wheel` if they're
   not installed already.

   .. warning::

      Be cautious if you're using a Python install that's managed by your
      operating system or another package manager. get-pip.py does not
      coordinate with those tools, and may leave your system in an
      inconsistent state. You can use ``python get-pip.py --prefix=/usr/local/``
      to install in ``/usr/local`` which is designed for locally-installed
      software.


Ensure pip, setuptools, and wheel are up to date
------------------------------------------------

While ``pip`` alone is sufficient to install from pre-built binary archives,
up to date copies of the ``setuptools`` and ``wheel`` projects are useful
to ensure you can also install from source archives::

    python -m pip install --upgrade pip setuptools wheel


Optionally, create a virtual environment
----------------------------------------

See :ref:`section below <Creating and using Virtual Environments>` for details,
but here's the basic `venv`_ [3]_ command to use on a typical Linux system:

.. code-block:: bash

    python3 -m venv tutorial_env
    source tutorial_env/bin/activate

This will create a new virtual environment in the ``tutorial_env`` subdirectory,
and configure the current shell to use it as the default ``python`` environment.


.. _`Creating and using Virtual Environments`:

Creating Virtual Environments
=============================

Python "Virtual Environments" allow Python :term:`packages <Distribution
Package>` to be installed in an isolated location for a particular application,
rather than being installed globally. If you are looking to safely install
global command line tools,
see :doc:`/guides/installing-stand-alone-command-line-tools`.

Imagine you have an application that needs version 1 of LibFoo, but another
application requires version 2. How can you use both these applications? If you
install everything into /usr/lib/python3.6/site-packages (or whatever your
platform’s standard location is), it’s easy to end up in a situation where you
unintentionally upgrade an application that shouldn’t be upgraded.

Or more generally, what if you want to install an application and leave it be?
If an application works, any change in its libraries or the versions of those
libraries can break the application.

Also, what if you can’t install :term:`packages <Distribution Package>` into the
global site-packages directory? For instance, on a shared host.

In all these cases, virtual environments can help you. They have their own
installation directories and they don’t share libraries with other virtual
environments.

Currently, there are two common tools for creating Python virtual environments:

* `venv`_ is available by default in Python 3.3 and later, and installs
  :ref:`pip` and :ref:`setuptools` into created virtual environments in
  Python 3.4 and later.
* :ref:`virtualenv` needs to be installed separately, but supports Python 2.7+
  and Python 3.3+, and :ref:`pip`, :ref:`setuptools` and :ref:`wheel` are
  always installed into created virtual environments by default (regardless of
  Python version).

The basic usage is like so:

Using `venv`_:

::

 python3 -m venv <DIR>
 source <DIR>/bin/activate

Using :ref:`virtualenv`:

::

 virtualenv <DIR>
 source <DIR>/bin/activate



For more information, see the `venv`_ docs or the `virtualenv <http://virtualenv.pypa.io>`_ docs.

In both of the above cases, Windows users should _not_ use the
`source` command, but should rather run the `activate` script directly
from the command shell. The use of `source` under Unix shells ensures
that the virtual environment's variables are set within the current
shell, and not in a subprocess (which then disappears, having no
useful effect).

Managing multiple virtual environments directly can become tedious, so the
:ref:`dependency management tutorial <managing-dependencies>` introduces a
higher level tool, :ref:`Pipenv`, that automatically manages a separate
virtual environment for each project and application that you work on.


Use pip for Installing
======================

:ref:`pip` is the recommended installer.  Below, we'll cover the most common
usage scenarios. For more detail, see the `pip docs <https://pip.pypa.io>`_,
which includes a complete `Reference Guide
<https://pip.pypa.io/en/latest/reference/index.html>`_.


Installing from PyPI
====================

The most common usage of :ref:`pip` is to install from the :term:`Python Package
Index <Python Package Index (PyPI)>` using a :term:`requirement specifier
<Requirement Specifier>`. Generally speaking, a requirement specifier is
composed of a project name followed by an optional :term:`version specifier
<Version Specifier>`.  :pep:`440` contains a :pep:`full
specification <440#version-specifiers>`
of the currently supported specifiers. Below are some examples.

To install the latest version of "SomeProject":

::

 pip install "SomeProject"


To install a specific version:

::

 pip install "SomeProject==1.4"


To install greater than or equal to one version and less than another:

::

 pip install "SomeProject>=1,<2"


To install a version that's :pep:`"compatible" <440#compatible-release>`
with a certain version: [4]_

::

 pip install "SomeProject~=1.4.2"

In this case, this means to install any version "==1.4.*" version that's also
">=1.4.2".


Source Distributions vs Wheels
==============================

:ref:`pip` can install from either :term:`Source Distributions (sdist) <Source
Distribution (or "sdist")>` or :term:`Wheels <Wheel>`, but if both are present
on PyPI, pip will prefer a compatible :term:`wheel <Wheel>`.

:term:`Wheels <Wheel>` are a pre-built :term:`distribution <Distribution
Package>` format that provides faster installation compared to :term:`Source
Distributions (sdist) <Source Distribution (or "sdist")>`, especially when a
project contains compiled extensions.

If :ref:`pip` does not find a wheel to install, it will locally build a wheel
and cache it for future installs, instead of rebuilding the source distribution
in the future.


Upgrading packages
==================

Upgrade an already installed `SomeProject` to the latest from PyPI.

::

 pip install --upgrade SomeProject


.. _`Installing to the User Site`:

Installing to the User Site
===========================

To install :term:`packages <Distribution Package>` that are isolated to the
current user, use the ``--user`` flag:

::

  pip install --user SomeProject


For more information see the `User Installs
<https://pip.readthedocs.io/en/latest/user_guide.html#user-installs>`_ section
from the pip docs.

Note that the ``--user`` flag has no effect when inside a virtual environment
- all installation commands will affect the virtual environment.

If ``SomeProject`` defines any command-line scripts or console entry points,
``--user`` will cause them to be installed inside the `user base`_'s binary
directory, which may or may not already be present in your shell's
:envvar:`PATH`.  (Starting in version 10, pip displays a warning when
installing any scripts to a directory outside :envvar:`PATH`.)  If the scripts
are not available in your shell after installation, you'll need to add the
directory to your :envvar:`PATH`:

- On Linux and macOS you can find the user base binary directory by running
  ``python -m site --user-base`` and adding ``bin`` to the end. For example,
  this will typically print ``~/.local`` (with ``~`` expanded to the absolute
  path to your home directory) so you'll need to add ``~/.local/bin`` to your
  ``PATH``.  You can set your ``PATH`` permanently by `modifying ~/.profile`_.

- On Windows you can find the user base binary directory by running ``py -m
  site --user-site`` and replacing ``site-packages`` with ``Scripts``. For
  example, this could return
  ``C:\Users\Username\AppData\Roaming\Python36\site-packages`` so you would
  need to set your ``PATH`` to include
  ``C:\Users\Username\AppData\Roaming\Python36\Scripts``. You can set your user
  ``PATH`` permanently in the `Control Panel`_. You may need to log out for the
  ``PATH`` changes to take effect.

.. _user base: https://docs.python.org/3/library/site.html#site.USER_BASE
.. _modifying ~/.profile: https://stackoverflow.com/a/14638025
.. _Control Panel: https://msdn.microsoft.com/en-us/library/windows/desktop/bb776899(v=vs.85).aspx

Requirements files
==================

Install a list of requirements specified in a :ref:`Requirements File
<pip:Requirements Files>`.

::

 pip install -r requirements.txt


Installing from VCS
===================

Install a project from VCS in "editable" mode.  For a full breakdown of the
syntax, see pip's section on :ref:`VCS Support <pip:VCS Support>`.

::

 pip install -e git+https://git.repo/some_pkg.git#egg=SomeProject          # from git
 pip install -e hg+https://hg.repo/some_pkg#egg=SomeProject                # from mercurial
 pip install -e svn+svn://svn.repo/some_pkg/trunk/#egg=SomeProject         # from svn
 pip install -e git+https://git.repo/some_pkg.git@feature#egg=SomeProject  # from a branch


Installing from other Indexes
=============================

Install from an alternate index

::

 pip install --index-url http://my.package.repo/simple/ SomeProject


Search an additional index during install, in addition to :term:`PyPI <Python
Package Index (PyPI)>`

::

 pip install --extra-index-url http://my.package.repo/simple SomeProject



Installing from a local src tree
================================


Installing from local src in `Development Mode
<https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode>`_,
i.e. in such a way that the project appears to be installed, but yet is
still editable from the src tree.

::

 pip install -e <path>


You can also install normally from src

::

 pip install <path>


Installing from local archives
==============================

Install a particular source archive file.

::

 pip install ./downloads/SomeProject-1.0.4.tar.gz


Install from a local directory containing archives (and don't check :term:`PyPI
<Python Package Index (PyPI)>`)

::

 pip install --no-index --find-links=file:///local/dir/ SomeProject
 pip install --no-index --find-links=/local/dir/ SomeProject
 pip install --no-index --find-links=relative/dir/ SomeProject


Installing from other sources
=============================

To install from other data sources (for example Amazon S3 storage) you can
create a helper application that presents the data in a :pep:`503` compliant
index format, and use the ``--extra-index-url`` flag to direct pip to use
that index.

::

 ./s3helper --port=7777
 pip install --extra-index-url http://localhost:7777 SomeProject


Installing Prereleases
======================

Find pre-release and development versions, in addition to stable versions.  By
default, pip only finds stable versions.

::

 pip install --pre SomeProject


Installing Setuptools "Extras"
==============================

Install `setuptools extras`_.

::

  $ pip install SomePackage[PDF]
  $ pip install SomePackage[PDF]==3.0
  $ pip install -e .[PDF]==3.0  # editable project in current directory


----

.. [1] "Secure" in this context means using a modern browser or a
       tool like `curl` that verifies SSL certificates when downloading from
       https URLs.

.. [2] Depending on your platform, this may require root or Administrator
       access. :ref:`pip` is currently considering changing this by `making user
       installs the default behavior
       <https://github.com/pypa/pip/issues/1668>`_.

.. [3] Beginning with Python 3.4, ``venv`` (a stdlib alternative to
       :ref:`virtualenv`) will create virtualenv environments with ``pip``
       pre-installed, thereby making it an equal alternative to
       :ref:`virtualenv`.

.. [4] The compatible release specifier was accepted in :pep:`440`
       and support was released in :ref:`setuptools` v8.0 and
       :ref:`pip` v6.0

.. _venv: https://docs.python.org/3/library/venv.html
.. _setuptools extras: https://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-extras-optional-features-with-their-own-dependencies
