
.. _projects:

=================
Project Summaries
=================

Python 설치 및 패키징에 있어서 가장 주요한 project들의 요약과 링크.

.. _pypa_projects:

PyPA Projects
#############

.. _bandersnatch:

bandersnatch
============

`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/bandersnatch/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/bandersnatch>`__ |
`PyPI <https://pypi.python.org/pypi/bandersnatch>`__

bandersnatch는 PyPI 미러링 클라이언트로, PyPI의 내용의 완전한 미러를 효율적으로 생성하도록 설계되었다.


.. _distlib:

distlib
=======

`Docs <http://pythonhosted.org/distlib/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/distlib/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/distlib>`__ |
`PyPI <https://pypi.python.org/pypi/distlib>`__

Distlib는 Python 소프트웨어의 packaging과 배포와 관련된 low-level function을 구현하는
라이브러리이다.


.. _packaging:

packaging
=========

`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/packaging/issues>`__ |
`Github <https://github.com/pypa/packaging>`__ |
`PyPI <https://pypi.python.org/pypi/packaging>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

Python packaging을 위해서 :ref:`pip` 과 :ref:`setuptools` 에 의해 사용되는 코어 유틸리티.


.. _pip:

pip
===

`Docs <https://pip.pypa.io/en/stable/>`__ |
`User list <http://groups.google.com/group/python-virtualenv>`__ [1]_ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/pip/issues>`__ |
`Github <https://github.com/pypa/pip>`__ |
`PyPI <https://pypi.python.org/pypi/pip/>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

Python package를 설치하기 위한 도구.


Python Packaging User Guide
===========================

`Docs <https://packaging.python.org/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ |
`Issues <https://github.com/pypa/python-packaging-user-guide/issues>`__ |
`Github <https://github.com/pypa/python-packaging-user-guide>`__ |
User irc:#pypa |
Dev irc:#pypa-dev

이 가이드!


.. _setuptools:
.. _easy_install:

setuptools
==========

`Docs <https://setuptools.readthedocs.io/en/latest/>`__ |
`User list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/setuptools/issues>`__ |
`GitHub <https://github.com/pypa/setuptools>`__ |
`PyPI <https://pypi.python.org/pypi/setuptools>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev


setuptools(``easy_install`` 을 포함)는 Python distribution을 더 쉽게 빌드하고 배포하기
위해 Python distutils의 향상된 기능 모음이다.

`distribute`_ 는 setuptools의 fork였으나 setultools의 v0.7에서 다시 merge되었다.
따라서 setuptools는 Python packaging에 가장 우선시되는 선택이다.


.. _twine:

twine
=====

`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://github.com/pypa/twine/issues>`__ |
`Github <https://github.com/pypa/twine>`__ |
`PyPI <https://pypi.python.org/pypi/twine>`__

Twine은 ``setup.py upload`` 를 대체 할 수 있는 PyPI와 안전하게 상호 작용하는 유틸리티이다.



.. _virtualenv:

virtualenv
==========

`Docs <https://virtualenv.pypa.io/en/stable/>`__ |
`User list <http://groups.google.com/group/python-virtualenv>`__ |
`Dev list <http://groups.google.com/group/pypa-dev>`__ |
`Issues <https://github.com/pypa/virtualenv/issues>`__ |
`Github <https://github.com/pypa/virtualenv>`__ |
`PyPI <https://pypi.python.org/pypi/virtualenv/>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev

격리 된 Python environment를 만들기위한 도구.


.. _warehouse:

Warehouse
=========

`Docs <https://warehouse.pypa.io/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://github.com/pypa/warehouse/issues>`__ |
`Github <https://github.com/pypa/warehouse>`__ |
Dev irc:#pypa-dev


새로운 미발매(unreleased) PyPI 응용 프로그램. https://pypi.org/에서 미리 볼 수 있다.


.. _wheel:

wheel
=====

`Docs <https://wheel.readthedocs.io/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bitbucket.org/pypa/wheel/issues?status=new&status=open>`__ |
`Bitbucket <https://bitbucket.org/pypa/wheel>`__ |
`PyPI <https://pypi.python.org/pypi/wheel>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev


주로 wheel 프로젝트는 :term:`wheel distributions <Wheel>` 을 만들기 위한 ``bdist_wheel`` :ref:`setuptools`
확장을 제공한다. 또한 wheel 생성 및 설치를 위한 자체 command line 유틸리티를 제공한다.


Non-PyPA Projects
#################

.. _bento:

bento
=====

`Docs <http://cournape.github.io/Bento/>`__ |
`Mailing list <http://librelist.com/browser/bento>`__ |
`Issues <https://github.com/cournape/Bento/issues>`__ |
`Github <https://github.com/cournape/Bento>`__ |
`PyPI <https://pypi.python.org/pypi/bento>`__

Bento는 distutils, setuptools, distribute 등의 대안으로 제안되는 python 소프트웨어 용
packaging tool solution이다. Bento의 철학은 순서대로 재현성, 확장성, 단순성이다.

.. _buildout:

buildout
========

`Docs <http://www.buildout.org/en/latest/>`__ |
`Mailing list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <https://bugs.launchpad.net/zc.buildout>`__ |
`PyPI <https://pypi.python.org/pypi/zc.buildout>`__ |
irc:#buildout

Buildout is a Python-based build system for creating, assembling and deploying
applications from multiple parts, some of which may be non-Python-based.  It
lets you create a buildout configuration and reproduce the same software later.

.. _conda:

conda
=====

`Docs <http://conda.pydata.org/docs/>`__

conda는 `Anaconda <http://docs.continuum.io/anaconda/index.html>`__ Python
설치를 위한 package 관리 도구이다. Anaconda Python은 특별히 과학계(특히 바이너리
extension 설치가 어려운 Windows)를 대상으로 `Continuum Analytics
<http://continuum.io/downloads>`__ 에서 내놓는 distribution이다.

Conda는 pip, virtualenv, wheel과는 완전해 별개의 도구이며, package관리, 가상환경 관리,
바이너리 extension의 배포 기능을 모아서 제공한다.

Conda는 PyPI에서 package를 설치하지 않으며, Continuum의 공식 repository,
사용자 제공 *conda* package를 관리하는 anaconda.org, 인트라넷과 같은 로컬 package
서버에서만 설치 가능하다. 그러나 PyPI에서의 distribution을 관리하기 위해 pip과 함께
사용이 가능하다.


devpi
=====

`Docs <http://doc.devpi.net/latest/>`__ |
`Mailing List <https://groups.google.com/forum/#!forum/devpi-dev>`__ |
`Issues <https://bitbucket.org/hpk42/devpi/issues>`__ |
`PyPI <https://pypi.python.org/pypi/devpi>`__

devpi는 강력한 PyPI 호환 서버 및 Python 프록시 캐시를 제공한다. 이와 함께 Python을 위한 
packaging, 테스트 및 릴리스 작업을 돕는 command line 도구를 제공한다.


flit
====

`Docs <https://flit.readthedocs.io/en/latest/>`__ |
`Issues <https://github.com/takluyver/flit/issues>`__ |
`PyPI <https://pypi.python.org/pypi/flit>`__

Flit is a simple way to put Python packages and modules on PyPI. Flit packages
a single importable module or package at a time, using the import name as the
name on PyPI. All subpackages and data files within a package are included
automatically. Flit requires Python 3, but you can use it to distribute modules
for Python 2, so long as they can be imported on Python 3.

enscons
=======

`Source <https://bitbucket.org/dholth/enscons/src>`__ |
`Issues <https://bitbucket.org/dholth/enscons/issues>`__ |
`PyPI <https://pypi.python.org/pypi/enscons>`__

Enscons is a Python packaging tool based on `SCons`_. It builds pip-compatible
source distributions and wheels without using distutils or setuptools,
including distributions with C extensions. Enscons has a different architecture
and philosophy than distutils. Rather than adding build features to a Python
packaging system, enscons adds Python packaging to a general purpose build
system. Enscons helps you to build sdists that can be automatically built by
pip, and wheels that are independent of enscons.

.. _SCons: http://scons.org/

.. _hashdist:

Hashdist
========

`Docs <https://hashdist.readthedocs.io/en/latest/>`__ |
`Github <https://github.com/hashdist/hashdist/>`__

Hashdist is a library for building non-root software distributions. Hashdist is
trying to be “the Debian of choice for cases where Debian technology doesn’t
work”. The best way for Pythonistas to think about Hashdist may be a more
powerful hybrid of virtualenv and buildout.

.. _pex:

pex
===

`Docs <https://pex.readthedocs.io/en/latest/>`__ |
`Github <https://github.com/pantsbuild/pex/>`__ |
`PyPI <https://pypi.python.org/pypi/pex>`__

pex is both a library and tool for generating ``.pex`` (Python EXecutable)
files, standalone Python environments in the spirit of :ref:`virtualenv`.
``.pex`` files are just carefully constructed zip files with a
``#!/usr/bin/env python`` and special ``__main__.py``, and are designed to make
deployment of Python applications as simple as ``cp``.

.. _spack:

Spack
=====

`Docs <http://software.llnl.gov/spack/>`__ |
`Github <https://github.com/llnl/spack/>`__ |
`Paper <http://www.computer.org/csdl/proceedings/sc/2015/3723/00/2807623.pdf>`__ |
`Slides <https://tgamblin.github.io/files/Gamblin-Spack-SC15-Talk.pdf>`__

A flexible package manager designed to support multiple versions,
configurations, platforms, and compilers.  Spack is like homebrew, but
packages are written in Python and parameterized to allow easy
swapping of compilers, library versions, build options,
etc. Arbitrarily many versions of packages can coexist on the same
system. Spack was designed for rapidly building high performance
scientific applications on clusters and supercomputers.

Spack is not in PyPI (yet), but it requires no installation and can be
used immediately after cloning from github.


Standard Library Projects
#########################

.. _ensurepip:

ensurepip
=========

`Docs <https://docs.python.org/3/library/ensurepip.html>`__ |
`Issues <http://bugs.python.org>`__

A package in the Python Standard Library that provides support for bootstrapping
:ref:`pip` into an existing Python installation or virtual environment.  In most
cases, end users won't use this module, but rather it will be used during the
build of the Python distribution.


.. _distutils:

distutils
=========

`Docs <https://docs.python.org/3/library/distutils.html>`__ |
`User list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <http://bugs.python.org>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev

A package in the Python Standard Library that has support for creating and
installing :term:`distributions <Distribution Package>`. :ref:`Setuptools`
provides enhancements to distutils, and is much more commonly used than just
using distutils by itself.


.. _venv:

venv
====

`Docs <https://docs.python.org/3/library/venv.html>`__ |
`Issues <http://bugs.python.org>`__

A package in the Python Standard Library (starting with Python 3.3) for
creating :term:`Virtual Environments <Virtual Environment>`.  For more
information, see the section on :ref:`Creating and using Virtual Environments`.


----

.. [1] pip was created by the same developer as virtualenv, and early on adopted
       the virtualenv mailing list, and it's stuck ever since.

.. [2] Multiple projects reuse the distutils-sig mailing list as their user list.


.. _distribute: https://pypi.python.org/pypi/distribute
