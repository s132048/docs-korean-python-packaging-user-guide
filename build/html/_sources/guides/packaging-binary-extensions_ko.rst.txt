.. _`Binary Extensions`:

===========================
바이너리 확장 패키징
===========================

:Page Status: Incomplete
:Last Reviewed: 2013-12-08

Cpython 참조 인터프리터의 특징 중 하나는 파이썬 코드를 허락하는 것은 물론, 다른 소프트웨어의 사용을 위해 좋은 C API 또한 이용할 수 있다. C API의 가장 일반적인 용도는 임포트할 수 있는 C 확장을 만드는 것이다. 이는 순수한 파이썬 코드만으로 쉽게 실행할 수 없는 것들을 가능하게 해준다.

.. contents:: Contents
   :local:

바이너리 확장 개요
================================

사용 사례  
---------

바이너리 확장의 일반적인 사용 사례는 3가지의 일반적인 카테고리로 나누어 진다.:



* accelerator modules: 이러한 모듈은 완전 독립식이고, CPython에서 실행되는 순수한 파  이썬 코드보다 더 빠르게 실행될 수 있게 작성되었다. 이상적으로, accelerator modul    e은 주어진 시스템에서 accelrated 버전을 사용할 수 없다면 대체물로 순수한 파이썬과   동일한 기능을 한다.  

* wrapper modules: 이러한 모듈은 파이썬 코드에 존재하는 C 인터페이스에 접근하기 위해  만들어졌다. 기초적인 C 인터페이스에 직접 노출시키거나, API를 사용하기 쉽게 만들어   주는 파이썬 언어의 특징을 사용하는 더 파이썬스러운 API에 노출을 시킨다. CPython 표  준 라이브러리는 래퍼 모듈을 광범위하게 사용할 수 있게 해준다. 

* low level system access: 이러한 모듈은 CPython 런타임, 운영체제 또는 기초적인 하드  웨어의 낮은 레벨의 특징에 접근하기 위해 만들어졌다. 플랫폼 특정 코드를 통해, 확장   모듈은 순수한 파이썬 코드로 할 수 없던 것을 얻을 수 있다. CPython 표준 라이브러리   모듈은 언어 수준에서 노출되지 않는 인터프리터 내부에 접근하기 위해 C로 작성되어졌   다. 

  C 확장의 주목할만한 특징은 인터프리터 런타임에서 콜백을 필요로 하지 않을 때, CPyth  on의 전역 인터프리터 잠금을 장기 실행 연산에 대해 릴리즈 할 수 있다는 것이다( 이러  한 연산이 CPU인지 IO bound인지에 대해 관계 없이) 


모든 확장 모듈이 깔끔하게 위의 카테고리에 맞아 떨어지는 것은 아니다. 예를 들어, NumPy를 포함하는 확장 모듈은 세 가지 케이스에 모두 적용된다. - 속도상의 이유로 내부 루프를 C로 이동시키고, C, FORTRAN 그리고 다른 언어로 작성된 외부 라이브러리를 래핑한다. 그리고 벡터화된 연산에 대한 동시 실행에 대한 지원과 생성된 object의 정확한 메모리 레이 아웃에 대한 제어를 위해 CPython과 기초적인 연산 시스템에서 낮은 수준의 시스템 인터페이스를 사용한다.


단점
-------------

바이너리 확장의 주된 단점은 소프트웨어의 후속 배포를 어렵게 한다는 것이다. 파이썬을 사용하는 이점 중 하나는 주로 크로스 플랫폼이다. 그리고 확장 모듈을 작성하는데 사용되는 언어(일반적으로 C 또는 C++, 그러나 CPython, C API에 바인딩할 수 있는 언어)는 일반적으로 커스텀 바이너리가 다른 플랫폼에서 만들어지는 것을 요구한다.

이는 바이너리 익스텐션을 의미한다.:

* 최종 사용자가 소스로부터 빌드하거나 일반 플랫폼 용으로 사전 빌드 된 바이너리를 게   시할 수 있어야한다.

* CPython 참조 인터프리터의 다른 빌드와 호환되지 않을 수 있다.

* PyPy, IronPython 또는 Jython과 같은 대체 해석기에서는 종종 정확하게 작동하지 않는   다.

* 핸드 코딩을 한 경우, 유지 보수자가 CPython이나 C API의 상세 사항 뿐만 아니라 바이   너리 확장에 사용된 파이썬이나 다른 언어에 익숙해지도록 요구함으로써 유지를 더욱 어  렵게 만든다.

* 순수한 파이썬 대체물 구현이 제공 된다면, 변경 사항을 두 곳에서 구현하도록 요구하고  양 쪽 버전이 항상 실행되도록 하기 위해 테스트 스위트에 추가적인 복잡성을 도입하여   유지 관리를 더 어렵게 만든다.

바이너리 확장에 의존하는 또 다른 단점은 대체 임포트 매커니즘(zipfile에서 직접 모듈을 임포트 하는 기능)은 종종 확장 모듈로 작동하지 않는다는 것이다.


핸드 코딩된 accelerator modules의 대안
---------------------------------------------

확장 모듈은 코드를 빨리 실행시키기 위해 사용된다.(프로파일링이 추가적인 유지 보수로 속도 향상이 있는 코드를 식별한 후) 또한 다른 많은 대안이 고려되어져야한다.:

* 기존의 최적화 된 대안을 찾는다. CPython 표준 라이브러리는 많은 최적화된 데이터 구   조와 알고리즘을 포함한다. (특히 ``collections`` 와 ``itertools`` 모듈 내에). 파이   썬 패키지 인덱스는 또한 추가적인 대안을 제공한다. 때때로, 표준 라이브러리나 써드    파티 모듈의 적절한 선택은 accelerator module 을 만드는 것을 피할 수 있게 해준다. 

* 오래 실행되는 애플리케이션의 경우, `PyPy 인터프리터 <http://pypy.org/>`__ 로 컴     파일된 JIT은 표준 CPython 실행시간에 적절한 대안을 제공할 수도 있다. PyPy를 채택하  는 주된 장벽은 일반적으로 다른 바이너리 확장 모듈에 의존한다. - PyPy는 CPython C A  PI를 에뮬레이트 하는 반면에, 거기에 의존하는 모듈들은 PyPy JIT에 문제를 일으킨다.   그리고 에뮬레이션 레이어는 종종 CPython이 현재 허용하고 있는 확장 모듈에 잠재적인   결함을 노출 시킬 수도 있다.(흔히 참조 카운팅 오류 주위에 - 두 개가 아닌 한 개의 참  조가 있는 object는 아무것도 손상시키지 않지만, 하나가 아닌 아무것도 참조 하지 않는  것은 큰 문제이다.)      

* `Cython <http://cython.org/>`__ 은 대부분의 Python 코드를 C 확장 모듈로 컴파일 할   수 있는 성숙한 정적인 컴파일러 이다. 초기 컴파일은 (CPython 인터프리터 레이어를 우  회하여) 약간의 속도 향상을 제공하며, Cython의 선택적 정적 타이핑 기능은 속도 향상   을 위한 추가 기회를 제공 할 수 있다. Cython을 사용하는 것은 여전히 결과 애플리케이  션을 배포하는 복잡성을 증가시키는 단점이 있지만 Python 프로그래머(C 또는 C++와  같  은 다른 언어와 비교하여)에 대한 진입 장벽을 낮출 수 있다는 이점이 있다. 

* `Numba <http://numba.pydata.org/>`__  는 과학적인 파이썬 커뮤니티의 멤버들이 만든   새로운 도구로, LLVM을 활용하여 파이썬 애플리케이션 조각의 선택적인 편집이 런타임시  원래의 코드를 따르게 하는 것이 목적이다.  LLVM은 코드가 실행되고 있는 시스템에서    이용 가능해야한다. 그러나 특히 벡터화가 가능한 연산의 경우에는 상당한 속도 향상을   제공할 수 있어야 한다.

핸드 코딩된 래퍼 모듈의 대안
-----------------------------------------

C ABI(Application Binary Interface)는 여러 애플리케이션들이 기능을 나누는 기본적인 표준이다. CPython C API의 강점 중 하나는 파이썬 유저가 기능을 사용할 수 있도록 허락해준다. 그러나 손을 직접하는 래핑 모듈은 꽤나 지루하다. 그래서 많은 대안 접근들이 고려되어야한다.

아래에 설명된 접근 방식은 배포 사례를 전혀 단순화 하지 않는다. 하지만 래퍼 모듈을 최신으로 유지하면서 유지 부담을 크게 줄일 수 있다.


* accelerator module의 생성에 유용하다. 또한, `Cython <http://cython.org/>`__  또한   래퍼 모듈을 만드는 데 유용하다. 그러나 여전히 손으로 인터페이스를 래핑하는 것이므   로 큰 API를 래핑하는 것은 좋은 선택이 아닐 수도 있다.

* `cffi <https://cffi.readthedocs.io/>`__  는 일부 PyPy개발자에 의해 만들어졌다. 그   리고 Python과 C를 이미 알고 있는 개발자가 Pyhon 애플리케이션에 C 모듈을 노출시키기  위해 만든 프로젝트이다. 또한 C를 모르더라도, 헤더 파일을 기반으로 C 모듈을 래핑하   는 것이 상대적으로 간단하다.

  ``cffi`` 의 이점 중 하나는 PyPy JIT과 호환이 된다는 것이다. CFFI 래퍼 모듈이 완전   히 PyPy의 트레이싱 JIT 최적화에 참가할 수 있게 해준다.

* `SWIG <http://www.swig.org/>`__  은 파이썬을 포함한 다양한 프로그래밍 언어가 C 와   C++ 코드를 인터페이스 할 수 있게 해주는 래퍼 인터페이스 제너레이터이다.

* 헤더 정보가 이용 불가능할 때, C 레벨의 인터페이스에 접근하는데 유용한 반면에, 표준  라이브러리의 ``ctypes`` 모듈은 C ABI 레벨에서만 작동한다. 그러므로 라이브러리에 의  해 실제로 엑스포트된 인터페이스와 파이썬 코드에서 선언된 인터페이스 사이에서 자동   으로 일관성을 체크하지 않는다. 반대로, 위의 대안은 인터페이스 사이의 일관성을 보장  하는 C 헤더 파일을 사용하면서 C API 레벨에서 모두 작동할 수 있다. ``cffi`` 가 C AB  I 레벨에서 직접 작동할 수 있지만, 그것은 ``ctypes`` 와 동일한 인터페이스 비일관성   문제가 된다.


낮은 수준의 시스템 접근을 위한 대안
----------------------------------------

이유에 관계없이 낮은 수준의 시스템 접근이 필요한 애플리케이션의 경우, 바이너리 확장 모듈을 사용하는 것이 가장 좋은 방법이다. 인터프리터가 코드를 실행하는 경우, 심지어 ctypes나 cffi 같은 모듈이 관련 C API 인터페이스에 대한 접근 권한을 획득하기 위해 사용되어 지는 경우,  전역 인터프리터 잠금과 같은 일부 연산이 단순히 유효하지 않기 때문에이는 특히 CPython 런타임 자체에 대한 낮은 수준의 접근이다. 

확장 모듈이 CPython 런타임 대신 기본 운영체제나 하드웨어를 조작하는 경우, 일반 C 라이브러리( C++ 또는 Rust 같은 다른 시스템 프로그래밍 언어)를 작성하는 것이 더 좋을수도 있다. 그리고 임포트가 가능한 파이썬 모듈로 사용할 수 있는 인터페이스를 만들기 위해 위에서 설명한 래핑 기술 중 하나를 사용한다. 


바이너리 확장을 구현하기 
==============================

CPython `확장 및 임베딩 <https://docs.python.org/3/extending/>`_
가이드는 `C에서 커스텀 확장 모듈 <https://docs.python.org/3/extending/extending.html>`_ 을 작성하는 것에 대한 소개를 포함하고 있다..

::

   mention the stable ABI (3.2+, link to the CPython C API docs)
   mention the module lifecycle
   mention the challenges of shared static state and subinterpreters
   mention the implications of the GIL for extension modules
   mention the memory allocation APIs in 3.4+

   mention again that all this is one of the reasons why you probably
   *don't* want to handcode your extension modules :)


바이너리 확장 빌드하기
==========================

윈도우에서 빌드 환경 세팅하기 
-----------------------------------------

바이너리 확장을 빌드하기 전에, 이용 가능한 적절한 컴파일러가 있어야 한다. 윈도우에서는 Visual C는 공식적인 CPython 인터프리터를 빌드하기 위해 사용된다. 그리고 호환이 되는 바이너리 확장을 빌드하는데 사용해야한다. 

파이썬 2.7은 비쥬얼 스튜디오 2008을 사용했고, 파이썬 3.3과 3.4는 비쥬얼 스튜디오 2010을 사용했다. 그리고 파이썬 3.5+는 비쥬얼 스튜디오 2015를 사용한다. 불행히도, 비쥬얼 스튜디오의 지난 버전은 더이상 쉽게 마이크로소프트에서 사용할 수 없다. 그래서 파이썬 3.5 이전의 버전에서는 더 이상 관련 버전의 비쥬얼 스튜디오의 사본이 없는 경우 컴파일러는 다르게 얻어져야한다.

바이너리 확장의 빌드 환경을 설정하기 위해, 다음의 단계를 따른다.:

    For Python 2.7

        1. Install "Visual C++ Compiler Package for Python 2.7",
           which is available from
           `Microsoft's website <https://www.microsoft.com/en-gb/download/details.aspx?id=44266>`__.
        2. Use (a recent version of) setuptools in your setup.py (pip will
           do this for you, in any case).
        3. Done.

    For Python 3.4

        1. Install "Windows SDK for Windows 7 and .NET Framework 4" (v7.1),
           which is available from
           `Microsoft's website <https://www.microsoft.com/en-gb/download/details.aspx?id=8279>`__.
        2. Work from an SDK command prompt (with the environment variables
           set, and the SDK on PATH).
        3. Set DISTUTILS_USE_SDK=1
        4. Done.

    For Python 3.5

        1. Install `Visual Studio 2015 Community Edition 
           <https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx>`__
           (or any later version, when these are released).
        2. Done.

파이썬 3.5 이후부터 비쥬얼 스튜디오는 backward 호환 방식으로 작동한다. 이는 비쥬얼 스튜디오의 후속 버전들은 3.5 이후의 모든 파이썬 버전을 위한 파이썬 확장을 빌드할 수 있을 것이다.

::

   FIXME

   cover Windows binary compatibility requirements
   cover macOS binary compatibility requirements
   cover the vagaries of Linux distros and other *nix systems



바이너리 확장 게시
============================

이 주제에 대한 중간 지침은
`여기 <https://github.com/pypa/python-packaging-user-guide/issues/284>`_ 를 참고 하면 된다.

::

   FIXME

   cover publishing as wheel files on PyPI or a custom index server
   cover creation of Windows and macOS installers
   mention the fact that Linux distros have a requirement to build from
   source in their own build systems, so binary-only releases are strongly
   discouraged
