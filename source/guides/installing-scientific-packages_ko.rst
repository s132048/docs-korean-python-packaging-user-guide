.. _`NumPy and the Science Stack`:

==============================
Installing Scientific Packages
==============================

:Page Status: Incomplete
:Last Reviewed: 2014-07-24

.. contents:: Contents
   :local:


과학 관련 소프트웨어는 대부분의 경우보다 복잡한 dependency를 갖는 경향이 있으며, 여러 종류의 하드웨어를
활용하거나 다른 외부 소프트웨어와 상호 운용하기 위해 여러 빌드 옵션을 제공하는 경우가 많다.

특히, `과학 관련 Python 스택 <http://www.scipy.org/stackspec.html#stackspec>`__
내의 대부분의 소프트웨어에 대한 기초를 제공하는 'NumPy <http://www.numpy.org/>`__
는 다른 FORTRAN 라이브러리들과 상호 운용되도록 설정 될 수 있으며, 현대 CPU에서 제공되는 다양한 레벨의
벡터화 instruction을 이용할 수 있다.

안타깝게도, 현재 2013년 12월을 기준으로, NumPy의 현재 빌드와 distribution 모델은 표준 도구를
사용하여 미리 빌드 된 NumPy 바이너리를 배포하는 작업과 호환되지 않는다. 또한 ``wheel`` 은 현재
설치프로그램이 Numpy 설치시에 사용자를 대신하여 결정을 내리는 것을 허용하지 않는다.

이 상황은 NumPy의 현재 빌드 및 배포 프로세스의 복잡성을 완전히 지원하도록 표준 도구의 개선 또는
NumPy 개발자가 하나의 빌드를 "가장 낮은 수용 가능한 공통 분모"로 선택하여 이를 PyPI에 wheel
파일로 publish하는 것을 통해 향후에 해결 될 것으로 예상된다.

그러나, 위의 방식대로 해결되기 전까지는 과학 관련 Python 라이브러리(또는 소스에서
설치하기 위한 환경이 필요하고 PyPI에 사전 빌드 된 wheel 파일을 제공하지 않는 다른
Python 라이브러리)를 설치하기 위한 여러 가지 대체 옵션이 있다.


Building from source
--------------------

NumPy(및 그것에 의존하는 많은 프로젝트)를 wheel 파일로 배포하는 것이 어려운 것과 같은 이유로 소스에서
직접 빌드하기는 어렵다. 그러나 C와 FORTRAN 모두에 대해 컴파일러와 링커를 다룰 용의가 있는 용감한
사람들에게는 소스에서 빌드하는 것도 옵션이다.


Linux distribution packages
---------------------------

Linux 사용자의 경우, 종종 시스템 패키지 관리자는 미리 컴파일 된 NumPy 및 과학 관련 Python 스택의
여러 부분을 이미 가지고 있다.

몇 개월이 지난 version을 사용하는 것이 허용된다면 이는 좋은 옵션이 될 수도 있다. 단, virtual
environment를 사용할 때에는 시스템 Python에 설치된 배포판에 대한 액세스를 허용해야 한다.


Windows installers
------------------

현재 wheel 파일을 publish하지 않는 (또는 못하는) 많은 Python 프로젝트는 PyPI 또는 프로젝트
다운로드 페이지에 Windows installer를 publish한다. 이러한 installer를 사용하면 사용자가
로컬에서 extension을 빌드하기 위한 적합한 environment을 구축할 필요가 없다.

이러한 installer에서 제공되는 extension은 일반적으로 python.org에 publish 된
CPython Windows installer와 호환된다.

Windows installer를 제공하지 않는 프로젝트의 경우, University of California의
Christoph Gohlke는 `collection of Windows installers
<http://www.lfd.uci.edu/~gohlke/pythonlibs/>`__ 를 제공한다. Windows상의
많은 Python 사용자들은 이러한 미리 빌드된 버전에 대해 긍정적인 경험을 보고했다.

Linux 시스템 패키지와 마찬가지로, Windows installer는 시스템 Python에만 설치된다.
가상 환경에서의 설치는 지원하지 않는다. 가상 환경을 사용할 때에는 시스템 Python에 설치된
배포판에 대한 액세스를 허용하는 것이 이러한 한계를 극복하기 위한 일반적인 접근법이다.

`wheel` 프로젝트는 Windows의 `bdist_wininst` installer를 wheel로 변환 할 수 있는
`wheel convert` subcommand 또한 제공한다.

.. preserve old links to this heading
.. _mac-os-x-installers-and-package-managers:

macOS installers and package managers
-------------------------------------

Windows와 마찬가지로 NumPy를 포함한 많은 프로젝트는 python.org에 publish된
macOS CPython 바이너리와 호환되는 macOS installer을 publish한다.

macOS 사용자는 "MacPorts"와 같은 Linux 배포 스타일 패키지 관리자에 액세스 할 수도 있다.
SciPy 사이트에는 MacPorts를 사용하여 `과학 관련 Python 스택 <http://www.scipy.org/install.html#mac-packages>`__ 설치하는 것에 대해 더 자세한 정보가 있다.


SciPy distributions
-------------------

SciPy 사이트에는 `여러 배포판 <http://www.scipy.org/install.html>`__ 을 통해
end user가 사용하기 쉽고 업데이트 하기 쉬운 형식으로 full SciPy stack을 제공한다.

이러한 배포판 중 일부는 표준 ``pip`` 이나 ``virtualenv`` 기반 toolchain과 호환되지 않을 수도
있다.

Spack
------
`Spack <https://github.com/LLNL/spack/>`_ 은 여러 버전, 설정, 플랫폼, 컴파일러를
지원 할 수 있도록 만들어진 유연한 패키지 관리자이다. 이는 소프트웨어를 여러가지
방법으로 빌드를 해야하는 대규모 슈퍼컴퓨팅 센터나 과학 어플리케이션 팀을 지원하기 만들어졌다.
Spack은 Python만에 한정되는 것은 아니다. ``C``, ``C++``, ``Fortran``, ``R``과 같은
언어들도 지원한다. Spack에서는 한 패키지의 새로운 버전을 설치하더라도
기존의 설치가 손상되지 않으므로, 한 시스템 내에 여러 구성으로 공존이 가능하다.

Spack은 사용자가 버전과 구성 옵션을 지정할 수 있는 간단하지만 강력한 syntax를 제공한다.
패키지 파일은 순수한 Python으로 작성되었으며, 단일 패키지 파일로 컴파일러,
MPI와 같은 종속성 구현, 버전, 빌드 옵션을 쉽게 swap 할 수 있도록 되어 있다.
또한 Spack은 *module* 파일을 생성하므로 사용자 환경에서 패키지를 로드하거나
언로드 할 수 있다.


The conda cross-platform package manager
----------------------------------------

`Anaconda <https://store.continuum.io/cshop/anaconda/>`__ 는 Continuum Analytics가
publish한 Python 배포판이다. 빅데이터와 과학적 사용을 위한 안정적인 오픈소스
패키지 모음이다. Anaconda 2.2와 함께 약 100개의 패키지가 설치되며 총
279개가 설치 및 업데이트가 Anaconda repository를 통해 가능하다. 

Anaconda에 포함 된 오픈 소스 패키지 관리 시스템 및 환경 관리 시스템인 "conda"는
사용자가 여러 버전의 바이너리 소프트웨어 패키지 및 dependency를 설치하고 이들 사이를
쉽게 전환 할 수있게 해준다. 이는 Windows, macOS 및 Linux에서 작동하는 cross-platform 도구이다.
Conda는 모든 종류의 패키지를 패키지화하고 배포하는 데 사용할 수 있으며, 이는 Python 패키지에만
국한되지 않는다. 또한 네이티브 가상 환경을 완벽하게 지원한다. Conda는 환경을
first-class citizen으로 만들어 독립적인 환경을 쉽게 만들 수 있다. 이것은 Python으로 작성되었지만
Python에 대해 독립적이다. Conda는 Python 자체를 패키지로 관리하므로 Python 패키지만 관리하는
pip과는 달리 `conda update python` 이 가능하다. Conda는 Anaconda와 Miniconda(Python과
conda만 포함)에서 사용할 수 있다. 
