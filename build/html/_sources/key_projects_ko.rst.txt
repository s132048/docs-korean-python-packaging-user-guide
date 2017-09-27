
.. _projects:

=================
프로젝트 요약
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

Distlib는 Python 소프트웨어의 packaging과 배포에 관련된 low-level function을 구현하는
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


setuptools(``easy_install`` 을 포함)는 Python distribution을 더 쉽게 빌드하고
배포하기 위해 Python distutils의 향상된 기능 모음이다.

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


주로 wheel 프로젝트는 :term:`wheel distributions <Wheel>` 을 생성하기 위한
``bdist_wheel`` :ref:`setuptools` extension을 제공한다. 또한 wheel 생성 및 설치를
위한 자체 command line 유틸리티를 제공한다.


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

Buildout은 여러 구성요소(non-Python 기반 포함)로 부터 응용 프로그램을 생성, 조합, 배포하기 위한
Python 기반 빌드 시스템이다. 빌드 설정을 만드는 것을 통해 나중에 같은 소프트웨어를 재생성 하는 것을
하게 해준다.

.. _conda:

conda
=====

`Docs <http://conda.pydata.org/docs/>`__

conda는 `Anaconda <http://docs.continuum.io/anaconda/index.html>`__ Python
설치를 위한 package 관리 도구이다. Anaconda Python은 특별히 과학계(특히 바이너리
extension 설치가 어려운 Windows)를 대상으로 `Continuum Analytics
<http://continuum.io/downloads>`__ 에서 내놓는 distribution이다.

Conda는 pip, virtualenv, wheel과는 완전해 별개의 도구이며, package 관리, 가상환경 관리,
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

devpi는 강력한 PyPI 호환 서버 및 Python 프록시 캐시 기능을 제공한다. 이와 함께 Python을 위한 
packaging, 테스트 및 릴리스 작업을 돕는 command line 도구를 제공한다.


flit
====

`Docs <https://flit.readthedocs.io/en/latest/>`__ |
`Issues <https://github.com/takluyver/flit/issues>`__ |
`PyPI <https://pypi.python.org/pypi/flit>`__

Flit은 Python의 package와 module을 PyPI에 올리는 간단한 방법이다. Flit은 import 이름을
PyPI의 이름으로 사용하여 한 번에 하나의 import 가능한 module 또는 package를 package화한다.
Package 내의 모든 subpackage 및 데이터 파일은 자동으로 포함된다. Flit에는 Python 3가 필요하지만
Python 3에서 import가 가능하다면 Python 2의 module을 배포하는 데 사용될 수도 있다.

enscons
=======

`Source <https://bitbucket.org/dholth/enscons/src>`__ |
`Issues <https://bitbucket.org/dholth/enscons/issues>`__ |
`PyPI <https://pypi.python.org/pypi/enscons>`__

Enscons는 `SCons`_ 에 기반한 Python packaging 도구이다. distutils 나 setuptools를
사용하지 않고 pip와 호환되는 (C extension을 가지는 distribution을 포함) source
distribution과 wheel을 빌드한다. Enscons는 distutils와는 다른 아키텍처와 철학을 가지고 있다.
Python packaging system에 빌드 기능을 추가하는 대신, enscons는 Python packaging을 범용
빌드 시스템에 추가한다. Enscons는 자동으로 pip로 빌드 될 수 있는 sdists와 enscons와는 독립적인
wheel을 만드는 데 도움을 준다.

.. _SCons: http://scons.org/

.. _hashdist:

Hashdist
========

`Docs <https://hashdist.readthedocs.io/en/latest/>`__ |
`Github <https://github.com/hashdist/hashdist/>`__

Hashdist는 non-root 소프트웨어 distribution을 빌드하기 위한 라이브러리이다.
Python 사용자가 Hashdist에 대해 생각하는 가장 좋은 방법은 virtualenv와 buildout의 더 강력한
하이브리드라고 생각하면 된다.

.. _pex:

pex
===

`Docs <https://pex.readthedocs.io/en/latest/>`__ |
`Github <https://github.com/pantsbuild/pex/>`__ |
`PyPI <https://pypi.python.org/pypi/pex>`__

pex는 :ref:`virtualenv` 의 정신을 따라서 독립 Python environment인 ``.pex`` (Python
EXecutable) 파일을 생성하는 라이브러리이자 도구이다. ``.pex`` 파일은 그저
``#!/usr/bin/env python`` 과 특별한 ``__main __. py`` 를 가진 신중하게 만들어진 zip
파일일 뿐이며, Python 응용 프로그램 배포를 ``cp`` 정도로 단순하게 만들도록 설계되었다.

.. _spack:

Spack
=====

`Docs <http://software.llnl.gov/spack/>`__ |
`Github <https://github.com/llnl/spack/>`__ |
`Paper <http://www.computer.org/csdl/proceedings/sc/2015/3723/00/2807623.pdf>`__ |
`Slides <https://tgamblin.github.io/files/Gamblin-Spack-SC15-Talk.pdf>`__

여러 버전, 설정, 플랫폼 및 컴파일러를 지원하도록 설계된 유연한 package 관리자.
Spack은 homebrew와 비슷하지만, package는 Python으로 작성되고 parameter화 되어
컴파일러, 라이브러리 버전, 빌드 옵션 등을 쉽게 교체하는 것을 허용한다. 임의로 많은 package version이
같은 시스템에 공존 할 수 있다. Spack은 클러스터와 슈퍼 컴퓨터에서 고성능 과학 응용 프로그램을
신속하게 구축 할 수 있도록 설계되었다.

Spack은 아직 PyPI에 없지만, 설치가 필요하지 않으며, github에서 cloning만으로 사용 할 수 있다.


Standard Library Projects
#########################

.. _ensurepip:

ensurepip
=========

`Docs <https://docs.python.org/3/library/ensurepip.html>`__ |
`Issues <http://bugs.python.org>`__

기존의 Python 설치 또는 가상 환경에 :ref:`pip` 의 bootstrapping을 지원하는
Python Standard Library의 package. 대부분의 경우 최종 사용자는 이 module을 사용하지 않고,
Python distribution을 빌드하는 동안만 사용된다.


.. _distutils:

distutils
=========

`Docs <https://docs.python.org/3/library/distutils.html>`__ |
`User list <http://mail.python.org/mailman/listinfo/distutils-sig>`__ [2]_ |
`Issues <http://bugs.python.org>`__ |
User irc:#pypa  |
Dev irc:#pypa-dev

:term:`distributions <Distribution Package>` 을 생성하고 설치하는 것을 지원하는
Python Standard Library 내의 package. :ref:`Setuptools` 가 distutils에 향상된 기능을
지원하며, distutils를 단독으로 사용하는 것 보다 훨씬 더 일반적으로 사용된다.


.. _venv:

venv
====

`Docs <https://docs.python.org/3/library/venv.html>`__ |
`Issues <http://bugs.python.org>`__

Python 3.3부터 :term:`Virtual Environments <Virtual Environment>` 를 생성하기 위한
Python Standard Library에 포함된 package. 더 자세한 정보는
:ref:`Creating and using Virtual Environments` 부분을 참조.


----

.. [1] pip는 virtualenv와 같은 개발자에 의해 만들어졌고, 초기에 virtualenv 메일링 리스트를 포함해
       버렸으며 그 이후로 계속 유지되어버렸다.

.. [2] 여러 프로젝트가 distutils-sig 메일링 리스트를 사용자 목록으로 재사용한다.


.. _distribute: https://pypi.python.org/pypi/distribute
