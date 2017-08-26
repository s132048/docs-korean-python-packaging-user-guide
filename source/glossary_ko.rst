========
Glossary
========


.. glossary::


    Binary Distribution

        특정 종류의 컴파일 된 extension을 포함하는 :term:`Built Distribution`.


    Built Distribution

        인스톨 하기 위해 올바른 위치에 옮기기만 해도 되는 파일과 메타데이터를 포함하는
:term:`Distribution <Distribution Package>` 포맷. :term:`Wheel` 은 여기에 포함되나
:term:`Source Distribution <Source Distribution (or "sdist")>` 은 인스톨 되기 전에
빌드 단계가 필요하므로 여기에 포함되지 않는다. 이 포맷은 Python 파일들이 pre-compile되어야
함을 의미하지는 않는다. (:term:`Wheel` 은 일부러 컴파일 된 Python 파일들을 포함하지 않는다)


    Distribution Package

        Python :term:`packages <Import Package>`, :term:`modules <module>`, 그리고 다른
:term:`Release` 를 배포하기 위한 리소스 파일들을 포함하는 버전관리 되는 아카이브.
아카이브 파일은 최종 사용자가 인터넷에서 다운로드 하고 인스톨 하는데 쓰인다.

        Distribution package이라는 용어 대신에 단순하게 주로 "package" 또는 "distribution"으로 불린다.
다만 여기에서는 마찬가지로 자주 "package"로 쓰이는 :term:`Import Package` 또는 "distribution"
으로 쓰이는 다른 distribution (Linux distribution이나 Python language distribution)과 혼동을
방지하기 위해서 필요시 확장된 용어를 쓰기도 한다.

    Egg

        :ref:`setuptools` 에 의해 도입된 :term:`Built Distribution`. 현재에는 :term:`Wheel` 로
대체되고 있다. 자세한 사항은 `The Internal Structure of Python Eggs
<https://setuptools.readthedocs.io/en/latest/formats.html>`_ 와
`Python Eggs <http://peak.telecommunity.com/DevCenter/PythonEggs>`_ 를 참조.

    Extension Module

        Python 구현의 low-level 언어로 쓰인 :term:`module`: Python을 위한 C/C++, Jython을 위한 Java.
주로 동적으로 로드 가능한 pre-compile된 하나의 파일에 포함된다: Unix에에서 shared object (.so) 파일,
Windows에서 .pyd확장자를 가지는 DLL 파일, file, Jython을 위한 Java class.


    Known Good Set (KGS)

        서로 호환되는 버전을 가진 distribution의 모음. 특정한 package 모음이 제대로 작동하는지
확인하기 위해 보통 여러 테스트를 통과해야 한다. 이 용어는 일반적으로 여러 distribution으로
이루어진 framework나 toolkit에 의해 쓰인다.


    Import Package

        다른 module을 포함하거나 재귀적으로 다른 package를 포함 할 수 있는 Python module.

        Import package는 일반적으로 "package"라고도 불리나, 이 가이드는 혼동을 방지하기 위해 필요시
확장된 용어를 사용한다.

    Module

        Python에서 재사용이 가능한 코드 단위. :term:`Pure Module` 와 :term:`Extension Module`
두가지 타입이 존재한다.


    Package Index

        :term:`package <Distribution Package>` 의 발견과 소비를 자동화 시키기 위해
web interface를 가지는 distribution의 repository.


    Per Project Index

        특정 :term:`Project` 가 종속성을 해결하기 위해 사용하는 개인 또는 비표준
:term:`Package Index`.


    Project

        :term:`Distribution <Distribution Package>` 로 package화 하기 위한 library, framework, script,
plugin, application, 또는 data나 resource의 모음.

        대부분의 project는 :ref:`distutils` 또는 :ref:`setuptools` 를 사용하여
:term:`Distributions <Distribution Package>` 를 생성하므로, project를 정의하기 위한
또 다른 실용적인 방법은 :term:`setup.py` 를 project의 src 디렉토리의 root에 포함하는
것을 무언가를 지칭하는 것이다. 여기에서 "setup.py" 는 :ref:`distutils` 와 :ref:`setuptools`
에 의해 쓰이는 project의 specification의 파일 이름이다.

        Python project는 :term:`PyPI <Python Package Index (PyPI)>` 에 등록되어 고유한 이름을
가져야 한다. 각 project는 그리고서 하나 이상의 :term:`Release <Release>` 를 포함하고,
각 :term:`Releases <Release>` 는 하나 이상의 :term:`distribution <Distribution Package>`
를 포함한다.

        Project를 실행하기 위해 import되는 package의 이름을 project의 이름으로 사용하는 강한 규약이 있다.
하지만 이는 꼭 지켜져야 하는 것은 아니다. 즉, 'foo'라는 project에서 distribution을 인스톨 하고
'bar'라는 import가능한 package를 제공 할 수도 있다.


    Pure Module

        하나의 .py (또는 .pyc, pyo) 파일에 포함되는 Python으로 쓰인 :term:`module`.


    Python Packaging Authority (PyPA)

        Python packaging과 관련된 여러 project를 관리하는 사람들 모임. https://www.pypa.io
사이트를 관리하고 project들을 `github <https://github.com/pypa>`_  와 `bitbucket
<https://bitbucket.org/pypa>`_ 에 호스팅 하며, `pypa-dev
mailing list <https://groups.google.com/forum/#!forum/pypa-dev>`_ 에서 문제들을 논의한다.


    Python Package Index (PyPI)

        `PyPI <https://pypi.python.org/pypi>`_ 는 Python 커뮤니티에서 default로 쓰는
:term:`Package Index` 이다. 모든 Python 개발자에게 distribution을 소비하거나
그들의 distribution을 배포하는 것에 오픈되어 있다.

    Release

        Version 식별이 있는 특정 시점에서의 :term:`Project` 의 스냅샷.

        Release를 만드는 것은 여러 :term:`Distribution <Distribution Package>` 의 publishing을
의미 할 수도 있다. 예를 들어, 만약 project의 version 1.0이 release 되었다면, 이는
source distribution과 Windows installer형식의 distribution을 모두 가질 수 있다.


    Requirement

       :term:`Package <Distribution Package>` 을 설치하기 위한 specification.
:term:`PYPA <Python Packaging Authority (PyPA)>` 에 의해 권장되는 installer인 :ref:`pip`은
"requirement"로 간주 될 수 있는 여러가지 형태의 specification을 허용한다.
:ref:`pip:pip install` 를 참조.


    Requirement Specifier

       :term:`Package Index` 에서 package를 설치하기 위해 :ref:`pip` 에서 사용되는 형식.
:ref:`setuptools` docs에서 `pkg_resources.Requirement
<https://setuptools.readthedocs.io/en/latest/pkg_resources.html#requirement-objects>`_
부분을 참조. 예를 들어, "foo>=1.3" 가 requirement specifier이다. 여기에서 "foo" 는 project 이름이고
">=1.3" 부분은 :term:`Version Specifier` 이다.

    Requirements File

       :ref:`pip` 을 사용하여 설치 가능한 :term:`Requirement <Requirement>` 들을 포함하는 파일로 된 목록.
더 자세한 사항은 :ref:`pip` docs의 :ref:`pip:Requirements Files` 부분을 참조.


    setup.py

        :ref:`distutils` 와 :ref:`setuptools` 을 위한 project의 specification 파일.


    Source Archive

        :term:`Source Distribution <Source Distribution (or "sdist")>` 또는 :term:`Built Distribution`
을 생성 하기 전, :term:`Release` 의 raw source code를 포함하는 아카이브.


    Source Distribution (or "sdist")

        :ref:`pip` 으로 설치하거나 :term:`Built Distribution` 을 생성하기 위한 metadata와
필수 소스 파일을 제공하는 일반적으로 ``python setup.py sdist`` 으로 생성된
:term:`distribution <Distribution Package>` 포맷.


    System Package

        운영 체제에 native한 format으로 제공되는 package. 예: rpm 또는 dpkg 파일.


    Version Specifier

       :term:`Requirement Specifier` 의 version 부분. 예를 들어, "foo>=1.3"의
">=1.3" 부분을 얘기한다. :pep:`440` 에는 Python packaging이 현재 지원하는
:pep:`full specification <440#version-specifiers>` 가 포함되어 있다. PEP440에 대한 지원은
:ref:`setuptools` v8.0과 :ref:`pip` v6.0에서 구현되었다.

    Virtual Environment

        Package가 시스템 전체에 설치되기보다는 특정 응용 프로그램에 의해 사용되도록 설치되는
격리 된 파이썬 환경. 자세한 정보는 :ref:`Creating and using Virtual Environments` 참조.

    Wheel

        :pep:`427` 에 의해 :term:`Egg` format을 대체하기 위해 도입된 :term:`Built Distribution` format. 
Wheel은 현제 :ref:`pip` 에 의해 지원된다.

    Working Set

        Import를 위해 제공되는 :term:`distribution <Distribution Package>` 모음.
`sys.path` variable상에 있는 distribution이다. 하나의 working set에는 project를 위한 :term:`distribution <Distribution Package>` 하나만 허용된다.
