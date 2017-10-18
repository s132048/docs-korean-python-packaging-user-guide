
=============================
Deploying Python applications
=============================

:Page Status: Incomplete
:Last Reviewed: 2014-11-11

.. contents:: Contents
   :local:


Overview
========


Supporting multiple hardware platforms
--------------------------------------

::

  FIXME

  의미: x86, x64, ARM, 기타?

  파이썬 전용 배포판의 경우, 파이선이 가동될 수 있는 모든 플랫폼에 배치(deploy)하는 것은
  간단해야 한다.

  바이너리 확장판로 이루어진 배포판의 경우 배치(deployment)가 가장 큰 문제다.
  확장판은 운영체제와 하드웨어 플랫폼의 모든 조합에 대해서 빌드되어 있어야 할 뿐 아니라,
  가급적 지속적인 통합 플랫폼에서 테스트도 이루어져야 한다. 이슈들은 위에 있는
  "multiple python versions" 섹션과 유사하며, 이것이 분리된 섹션이 되어야 하는지는
  확실하지 않다. 윈도우즈 x64에서도 32 bit와 64 bit 버전의 파이썬을 사용할 수 있다.



OS Packaging & Installers
=========================

::

  FIXME

  - 프로젝트를 위한 rpm/debs 빌드하기
  - 모든 가상환경을 위한 rpms/debs 빌드하기
  - 파이썬 프로젝트를 위한 macOS installers 빌드하기
  - Kivy+P4A or P4A & Buildozer로 Android APKs 빌드하기

Windows
-------

::

  FIXME

  - 파이썬 프로젝트를 위한 Windows installers 빌드하기

Pynsist
^^^^^^^

`Pynsist <https://pypi.python.org/pypi/pynsist>`__ 는 파이썬 프로그램을 파이썬
인터프리터와 함께 NSIS를 기반으로 하는 단일 인스톨러(installer)에 집어 넣는(bundle)
툴(tool)이다. 대부분의 경우에 패키징은 사용자에게 파이선 인터프리터의 버전을 선택하고
프로그램의 의존성을 지정하는 것만을 요구한다. 이 윈도우즈 용 특정 파이썬 인터프리터를
다운로드 하고 단일 윈도우즈 실행가능 인스톨러에 모든 의존성을 패키징한다.

인스톨러는 사용자 시스템에 파이썬 인터프리터를 설치하고 업그레이드 하며 패키지된
프로그램과 관계없이 사용될 수 있다. 프로그램은 시작메뉴에 있는 숏컷(shortcut)으로
시작할 수 있다. 프로그램 제거는 사용자의 파이썬 설치를 손상시키지 않는다.

Pynsist의 장점은 윈도우즈 패키지가 리눅스에서 빌드될 수 있다는 것이다.
`documentation <https://pynsist.readthedocs.io>`__\ 에 여려 종류의
프로그램(console, GUI)에 대한 다양한 예시가 있다. 툴은 MIT-licence 하에서 공개되었다.

Application Bundles
===================

::

  FIXME

  - py2exe/py2app/PEX
  - wheels kinda/sorta


Configuration Management
========================

::

  FIXME

  puppet
  salt
  chef
  ansible
  fabric
