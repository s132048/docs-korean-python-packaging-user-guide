.. _`Tool Recommendations`:

====================
도구 추천
====================

만약 파이썬 패키징과 설치에 익숙하고 어떤 도구가 현재 추천되는지 알고 싶다면, 바로 여기에 있다.


설치 도구 추천 
=================================

* :ref:`pip` 를 사용해서 :term:`packages <Distribution Package>` 부터  
  :term:`PyPI <Python Package Index (PyPI)>` 까지의 파이썬을 설치해라. [1]_ [2]_ :ref:`pip`
  가 어떻게 설치됐는지에 따라 wheel 캐싱을 사용하기 위해 :ref:`wheel` 을 추가적으로 설치해야 할 수도 있다. [3]_

* :ref:`virtualenv` 나 `venv`_  을 사용해 공용 파이썬 설치와 특정 종속성을 가진 애플리케이션과 분리시킨다. [4]_

* 통합된 교차 플랫폼 스포트웨어 스택을 관리하는 것을 찾고 싶다면, :

  * 웹 개발 커뮤니티에서 집중하는 :ref:`buildout` 와 :  

  * 과학 커뮤니티에서 집중하는 :ref:`spack`, :ref:`hashdist` 또는 :ref:`conda` 을 고려해라: 



패키징 도구 추천
==============================

* :ref:`setuptools` 을 사용하여 프로젝트를 확정하거나 :term:`Source Distributions
  <Source Distribution (or "sdist")>`. [5]_ [6]_ 을 만들어라.

* :ref:`wheel project <wheel>` 을 통해 사용할 수 있는 ``bdist_wheel`` :ref:`setuptools`  확장판     
  을 사용해 :term:`wheels <Wheel>` 을 생성해라. 이는 특히 프로젝트가 바이너리 확장을 포함하고 있는 경우 유용하  
  다. [7]_

* :term:`PyPI <Python Package Index (PyPI)>` 로 업로드 하는 배포판을 위해 `twine <https:// 
  pypi.python.org/pypi/twine>`_ 를 사용해라.


플랫폼 마이그레이션 발행
=============================

기본 파이썬 패키지 지수 구현( `pypi.python.org <https://pypi.python.org>`_ 를 통해 소개되는)은  `pypi.org <https://pypi.org>`_ 에서 소개되는 상향된 구현버전으로 인해 단계적으로 폐기되고 있다. 두 인터페이스 모두 공통 데이터베이스 백엔드와 파일 보관함을 쓰지만, 후자 사용이 더 용이해질수록 기본값 책임도가 더 높아질 것이다.

위에서 추천된 도구의 최선버전을 기본값 세팅으로 사용하는 유저들은 이 마이그레이션에 대해 걱정할 필요가 없지만, 구형 버전이나, 기본값 세팅을 사용하지 않는 유저라면 조작법을 업데이트하고 아래의 추천을 따라야 한다.

퍼블리싱 출시 
-------------------

``pypi.org`` 는 2016년 9월부터 기본 업로딩 플랫폼이 되었다.

``pypi.python.org`` 을 통한 업로드는 2017년 7월 3일부로 *중지* 될 것이다.

아래의 버전에서 기본 업로딩 세팅은 ``pypi.org`` 으로 변경되었다. :

* ``twine`` 1.8.0
* ``setuptools`` 27.0.0
* Python 2.7.13 (``distutils`` update)
* Python 3.4.6 (``distutils`` update)
* Python 3.5.3 (``distutils`` update)
* Python 3.6.0 (``distutils`` update)


브라우징 패키지
-----------------

``pypi.python.org`` 는 여전히 브라우징 패키지에 있어 기본 인터페이스로 사용된다.
(다른 PyPA documentation, 등의 링크에서 사용됨).

``pypi.org`` 는 가능한 패키지를 브라우징 하는 목적으로 충분히 실용적이고, 몇몇의 유저들은 그것을 사용하기를 선택할 수도 있다.

이후에 두 섹션의 한계점이 소개된 후 ``pypi.org`` 는 브라우징 인터페이스로서 기본값으로 추천될 것으로 예상된다. (어느 순간부터 ``pypi.python.org`` 을 사용하려는 시도가 자동적으로 ``pypi.org`` 로 변경될 것)


패키지 다운로딩
--------------------

``pypi.python.org`` 는 현재 여전히 패키지 다운로딩을 위한 기본값의 호스트이다.

``pypi.org`` 는 패키지를 다운로드 하는 목적으로는 충분히 구동 가능하고 몇몇의 유저들은 그것을 사용하기를 선택할 수 있다. 하지만 그것의 현재 호스팅 셋업은 기본값 다운로드 소스가 되기 위해 전체 대역폭을 처리하는 것을 감당할 수 없다. (설사 빠른 CDN을 포함시킨다 하여도)

``pypi.org`` 는 연관된 네트워크 로드를 처리하는 것을 감당할 수 있는 환경으로 이동된 이후 패키지 다운로딩의 기본값 호스트가 될 것이다.

릴리즈와 퍼블리싱 패키지 관리 
----------------------------------------

``pypi.python.org`` 는 로그인 된 유저들에게 출고 된 패키지와 출시 관리 인터페이스를 제공한다.

``pypi.org`` 는 현재 그런 인터페이스가 제공되지 않는다.

잃어버린 기능들은 `Shut Down Legacy PyPI <https://github.com/pypa/warehouse/milestone/7>`_ 
마일스톤의 일부분으로 추적되고 있다.


----

.. [1] :term:`Eggs <Egg>` (pip가 지원하지 않는)를 통해 설치해야 한다면 ``easy_install``  (from :ref:`setuptools` ), e.g. 를 사용해야 하는 경우가 생길 수도 있다. 자세한 내용은 :ref:`pip vs easy_install` 을 보세요.

.. [2] :pep:`453` 이 받아들여지는 것은 :ref:`pip` 이 파이썬 3.4나 그 이후 버전에서 기본값으로 사용가능 하다는 것을 뜻한다. :pep:`453` 의 :pep:`rationale section <453#rationale>` 를 통해 왜 pip가 선택됐는지 확인해라.

.. [3] :ref:`get-pip.py <pip:get-pip>` 와 :ref:`virtualenv` 는 :ref:`wheel` 를 설치하지만, :ref:`ensurepip` 와 :ref:`venv <venv>` 는 현재는 그렇지 않다. 또한, 리눅스 디스트로스에서 찾을 수 있는 기본 "python-pip" 패키지는 현재 "python-wheel"에 의존하지 않는다.

.. [4] Python 3.4, ``venv`` 로 시작하면 ``pip`` 가 설치 된 virtualenv 환경을 만들 것인데, 이것은 :ref:`virtualenv` 와 동등한 대체가 된다. 하지만, :ref:`virtualenv` 를 사용하는 것은 여전히 교차-버전 지속도가 필요한 유저들에게 권장된다.

.. [5] 비록 순정 ``distutils`` 을 많은 프로젝트에 사용할 수 있지만, 그것은 다른 프로젝트를 정의하는 의존성을 지원하지 않고 ``setuptools`` 에 의해 제공되는 자동으로 채워지는 분배 메타데이터를 올바르게 사용하기 위한 몇 가지 유용한 도구를 빠트리고 있다. 기본 라이브러리 밖에 있기 때문에 ``setuptools`` 는 파이썬의 다른 버전들에 더 연계된 기능들을 제공하고, (``distutils`` 과는 다르게) ``setuptools`` 는 앞으로 나올 "Metadata 2.0" 기본 포멧을 모든 버전에서 제공하기 위해 업데이트 될 것이다.

    ``distutils`` 을 사용하기로 선택한 프로젝트에도 :ref:`pip` 가 직접 소스에서 특정 프로젝트를 설치할 시(이미    
    만들어진 :term:`wheel <Wheel>` 파일에서 설치를 하기보다), :ref:`setuptools` 를 대신 사용해 당신의 프   
    로젝트를 만들 것이다.

.. [6] `distribute`_ (a fork of setuptools)는 :ref:`setuptools` 로 2013년 6월에 재병합 됐는데, 이것은 셋업툴이 패키징에 기본값으로 선택되게 만들었다.

.. [7] :term:`PyPI <Python Package Index (PyPI)>` 은 현재 Windows and macOS 휠만 업로딩이 되도록 허락하고, 그것은 python.org에서 다운로드를 통해 제공되는 바이너리 인스톨러와 호환이 되어야 한다. 리눅스 휠이 허용되기 전에 :pep:`wheel compatibility tagging scheme<425>` 의 향상이 되어야 한다.

.. _distribute: https://pypi.python.org/pypi/distribute
.. _venv: https://docs.python.org/3/library/venv.html
