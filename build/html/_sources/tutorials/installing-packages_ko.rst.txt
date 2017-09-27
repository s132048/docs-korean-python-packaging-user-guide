===================
패키지 설치하기
===================

이 섹션은 파이썬 :term:`packages <Distribution Package>` 설치 방법의 기본을 다룬다.

이 맥락에서 용어 "패키지"는 :term:`distribution <Distribution Package>`
(설치되는 소프트웨어 번들(bundle))의 동의어로서 사용되고 있다는 사실을 유의하라.
파이썬 소스 코드에서 임포트 하는 :term:`package <Import Package>` (모듈 컨테이너)
같은 것을 의미하는 것이 아니다. 파이썬 커뮤니티에서는 :term:`distribution
<Distribution Package>`\ 를 "패키지"라고 언급하는 일이 일반적이다.
"distribution"이라는 용어를 사용하는 것은 권장되지 않는다. 왜냐하면,
리눅스 distribution이나 파이썬 같은 다른 큰 소프트웨어 distribution과 쉽게 혼동을
일으킬 수 있기 때문이다.


.. contents:: 목차
   :local:


.. _installing_requirements:

패키치 설치를 위한 요구조건
====================================

이 섹션은 다른 파이썬 패키지를 설치하기 전에 따라야 할 단계에 대해 설명하고 있다.

pip, setuptools, wheel 설치하기
----------------------------------

* 만약 `python.org <https://www.python.org>`_\ 에서 파이썬 3 >=3.4 또는 파이썬
  2 >= 2.7.9 를 설치했다면 당신은 이미 :ref:`pip`\ 와 :ref:`setuptools`\ 가 있을
  것이다. 하지만 최신 버전으로 업그레이드 해주어야 한다:

  리눅스 또는 맥 OS:

  ::

    pip install -U pip setuptools


  윈도우즈:

  ::

    python -m pip install -U pip setuptools

* 만약 시스템 패키지 매니저(예, "yum", "apt-get" 등)에 의해 관리되는 리눅스에 설치된
  파이썬을 사용하고 있고 시스템 패키지 매니저를 이용해 pip를 설치하고 업그레이드하고
  싶다면 :ref:`Installing pip/setuptools/wheel with Linux Package Managers`\ 를
  참고하라.

* 다른 경우:

 * 안전하게 `get-pip.py <https://bootstrap.pypa.io/get-pip.py>`_ [1]_\ 를
   다운로드 하라.

 * ``python get-pip.py`` [2]_\ 를 실행하면 pip를 설치하거나 업그레이드해 줄 것이다.
   아직 설치되어있지 않으면 추가적으로 :ref:`setuptools`\ 와 :ref:`wheel`\ 도 설치할
   것이다.

   .. warning::

      만약 당신의 운영체제나 다른 패키지 매니저에 의해 관리되는 파이썬을 사용하고
      있으면 get-pip.py는 위의 툴들과 조화를 이루지 못하고 시스템을 일관성이
      유지되지 않는 상태로 만들 것이다. 이 경우 ``python get-pip.py
      --prefix=/usr/local/``\ 를 사용해서 로컬에 설치되는 소프트웨어를 위해
      고안된 ``/usr/local``\ 에 설치하라.


선택적으로, 가상 환경을 생성하기
----------------------------------------

자세한 사항은 :ref:`아래에 있는 섹션 <Creating and using Virtual Environments>`\ 을
참고해야 하지만 기본적인 커맨드는 여기에 있다:

   :ref:`virtualenv` 사용하기:

   ::

    pip install virtualenv
    virtualenv <DIR>
    source <DIR>/bin/activate

   `venv`_ 사용하기: [3]_

   ::

    python3 -m venv <DIR>
    source <DIR>/bin/activate


#.. _`Creating and using Virtual Environments`:

가상 환경 생성하기
=============================

파이썬 "가상 환경"은 파이썬 :term:`packages <Distribution Package>`\ 가 글로벌하게
(globally) 설치되지 않고 특정한 어플리케이션을 위한 독립된 위치에 설치되게 할 수 있다.

당신이 LibFoo 버전 1을 필요로 하는 어플리케이션을 가지고 있다고 상상해보자, 그런데
다른 어플리케이션은 버전 2를 요구한다. 어떻게 두 가지 어플리케이션을 다 쓸 수 있을까?
만약 당신이 모든 것을 /usr/lib/python2.7/site-packages (또는 플랫폼의 표준 로케이션)
에 설치했다면 업그레이드 하지 말아야 할 어플리케이션을 의도치 않게 업그레이드 하는
상황에 맞닥뜨릴 수 있다.

또는 더 일반적으로, 어플리케이션을 설치한 뒤 그대로 놔두길 원한다면? 만약
어플리케이션이 작동하면, 라이브러리나 라이브러리 버전의 변화가 어플리케이션을
망가뜨릴 수 있다.

또한, :term:`packages <Distribution Package>`\ 를 글로벌 site-packages 디렉토리에
깔 수 없다면? 예를 들면, 호스트를 공유하고 있는 경우.

이러한 모든 경우에, 가상 환경이 도움이 될 수 있다. 가상 환경은 모두 개별적인 설치
디렉토리를 가지고 있고, 다른 가상환경과 라이브러리를 공유하지 않는다.

현재, 파이썬 가상환경 구축을 위해 사용가능한 들은 두 가지가 있다. Currently, there are two viable tools for creating Python virtual environments:

* `venv`_\ 는 파이썬 3.3 이후의 버전에서 기본으로 이용 가능하며, 3.4 이후의 버전에서는
  :ref:`pip`\ 와 :ref:`setuptools` 를 생성된 가상환경에 설치한다.
* :ref:`virtualenv`\ 는 따로 설치되어야 하지만 파이썬 2.6 이상, 3.3 이상을 지원하며,
  :ref:`pip`\, :ref:`setuptools`, :ref:`wheel`\ 는 기본으로 (파이썬 버전과
  관계없이) 생성된 가상 환경에 설치된다.

기본적인 사용방법은 아래와 같다:

:ref:`virtualenv` 사용하기:

::

 virtualenv <DIR>
 source <DIR>/bin/activate


`venv`_ 사용하기:

::

 python3 -m venv <DIR>
 source <DIR>/bin/activate


더 상세한 정보는, `virtualenv <http://virtualenv.pypa.io>`_\ 나 `venv`_ 문서를
참고하라.


설치를 위해 pip 사용하기
=========================

:ref:`pip`\ 는 권장되는 인스톨러(installer). 아래에, 우리는 가장 일반적인 사용
시나리오를 다룰 것이다. 더 자세한 정보는 완전한 `레퍼런스 가이드
<https://pip.pypa.io/en/latest/reference/index.html>`_\ 를 포함하는
`pip 문서 <https://pip.pypa.io>`_\ 를 참고하라.

pip 대신에 `easy_install <https://pip.pypa.io/en/latest/reference/index.html>`_
을 사용하기를 원하는 경우가 있다. 자세한 정보는 :ref:`pip vs easy_install`\ 를
참고하라.


PyPI에서 설치하기
====================

가장 일반적인 :ref:`pip`\ 사용법은 :term:`requirement specifier
<Requirement Specifier>`\ 를 사용하는 :term:`Python Package
Index <Python Package Index (PyPI)>`\ 로부터 설치하는 것이다. 일반적으로 요구사항
지정자(requirement specifier)는 프로젝트 이름과 선택적인 :term:`version specifier
<Version Specifier>`\ 로 구성되어 있다. :pep:`440`\ 는 현재 지원되는 지정자의
:pep:`전체 목록 <440#version-specifiers>`\ 를 포함하고 있다. 아래는 몇 가지
예시들이다.

"SomeProject"의 최신 버전 설치:

::

 pip install 'SomeProject'


특정한 버전 설치:

::

 pip install 'SomeProject==1.4'


버전 1 이상, 2 미만 설치:

::

 pip install 'SomeProject>=1,<2'


특정한 버전과 :pep:`"호환 되는" <440#compatible-release>` 버전 설치 : [4]_

::

 pip install 'SomeProject~=1.4.2'

이 경우, 이는 ">=1.4.2"인 아무 "==1.4.*" 버전을 설치하는 것을 의미한다.
.


소스 배포판 vs wheels
==============================

:ref:`pip`\ 는 :term:`Source Distributions (sdist) <Source
Distribution (or "sdist")>` 또는 :term:`Wheels <Wheel>`\ 로부터 설치할 수 있지만,
둘 다 PyPI에 있다면 pip는 호환 되는 :term:`wheel <Wheel>`\ 을 선호한다.

:term:`Wheels <Wheel>`\ 는 :term:`Source Distributions (sdist) <Source
Distribution (or "sdist")>`\ 과 비교했을 때 (특히 컴파일된 확장자가 있을 떄)
훨씬 더 빠르게 설치할 수 있는 프리 빌드된(pre-built) :term:`distribution
<Distribution Package>` 포맷이다.

만약 :ref:`pip`\ 가 설치할 wheel을 찾지 못하면, pip는 나중에 source distribution
을 리빌딩 하는 대신 로컬에서 미래에 설치할 wheel을 빌드하고 저장(cache)해둔다.
in the future.


패키지 업그레이드 하기
=========================

PyPI로부터 설치된 `SomeProject`\ 를 최신 버전으로 업그레이드하기.

::

 pip install --upgrade SomeProject



사용자 사이트에 설치하기
===========================

현재 사용자와 분리된 :term:`packages <Distribution Package>`\ 설치하려면
``--user`` 플래그(flag)를 사용하라:

::

  pip install --user SomeProject


더 자세한 정보는 pip 문서에 있는 `User Installs
<https://pip.readthedocs.io/en/latest/user_guide.html#user-installs>`_\ 를
참고하라.


요구조건 파일
==================

:ref:`Requirements File <pip:Requirements Files>`\ 에서 지정된 요구 사항 목록
설치.

::

 pip install -r requirements.txt


VCS에서 설치하기
===================

"편집" 모드에서 VCS에 있는 프로젝트 설치. 신택스에 대한 전제 내용은
:ref:`VCS Support <pip:VCS Support>`\ 에 있는 pip 섹션을 참고하라.

::

 pip install -e git+https://git.repo/some_pkg.git#egg=SomeProject          # from git
 pip install -e hg+https://hg.repo/some_pkg.git#egg=SomeProject            # from mercurial
 pip install -e svn+svn://svn.repo/some_pkg/trunk/#egg=SomeProject         # from svn
 pip install -e git+https://git.repo/some_pkg.git@feature#egg=SomeProject  # from a branch


다른 색인에서 설치하기
=============================

대체 색인으로부터 설치

::

 pip install --index-url http://my.package.repo/simple/ SomeProject


:term:`PyPI <Python Package Index (PyPI)>`\ 를 포함해 설치 중 추가적인 색인
검색

::

 pip install --extra-index-url http://my.package.repo/simple SomeProject



로컬 소스 트리에서 설치하기
================================


`Development Mode
<https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode>`_
에 있는 로컬 소스로부터 설치, 즉 이러한 방식은 프로젝트가 설치된 것으로 나타나지만
여전히 소스 트리에서 편집 가능하다.

::

 pip install -e <path>


소스에서 평범하게 설치할 수도 있다.

::

 pip install <path>


로컬 아카이브에서 설치하기
==============================

특정한 소스 아카이브 파일 설치.

::

 pip install ./downloads/SomeProject-1.0.4.tar.gz


아카이브를 포함한 로컬 디렉토리로부터 설치(:term:`PyPI
<Python Package Index (PyPI)>` 확인하지 않음)

::

 pip install --no-index --find-links=file:///local/dir/ SomeProject
 pip install --no-index --find-links=/local/dir/ SomeProject
 pip install --no-index --find-links=relative/dir/ SomeProject


다른 소스에서 설치하기
=============================

다른 데이터 소스로부터 설치하기 위해서(예, 마아마존 S3 저장소) 당신은 색인 포맷을
따르는 :pep:`503`\ 에 있는 데이터를 제공하는 helper application을 생성할 수 있으며
``--extra-index-url`` 플래그를 사용해서 pip가 그 색인을 사용하도록 지시할 수 있다.

::

 ./s3helper --port=7777
 pip install --extra-index-url http://localhost:7777 SomeProject


프리 릴리즈
======================

안정된 버전을 포함해 프리 릴리즈, 개발자 버전을 찾아라. 기본적으로 pip는 안정된
버전만 찾는다.

::

 pip install --pre SomeProject


Setuptools "Extras" 설치하기
==============================

`setuptools extras`_\  설치.

::

  $ pip install SomePackage[PDF]
  $ pip install SomePackage[PDF]==3.0
  $ pip install -e .[PDF]==3.0  # editable project in current directory



----

.. [1] 이 문맥에서 "안전하게"는 최신 브라우저나 https URL에서 다운로드 할 때
       SSL 인정스럴 확인하는 `curl`\ 같은 툴을 사용하는 것을 말한다.

.. [2] 플랫폼에 따라 루트나 관리자 권한이 필요할 수 있다.
       :ref:`pip`\ 는 `사용자 installs를 디폴트 작동으로 만들어서
       <https://github.com/pypa/pip/issues/1668>`_ 이것을 바꾸는 것을
       고려하고 있다.

.. [3] Python 3.4로 시작하면, ``venv`` (:ref:`virtualenv`\ 의 대체 표준 라이브러리)
       가 설치된 ``pip``\ 로 가상 환경을 생성하고, 그렇게 함으로써
       :ref:`virtualenv`\ 와 동일한 대체재가 될 것이다. .

.. [4] 호환되는 릴리즈 지정자는 :pep:`440`\ 에서 승인되었고, 지원은
       :ref:`setuptools` v8.0, :ref:`pip` v6.0\ 에서 공개 되었다.

.. _venv: https://docs.python.org/3/library/venv.html
.. _setuptools extras: https://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-extras-optional-features-with-their-own-dependencies
