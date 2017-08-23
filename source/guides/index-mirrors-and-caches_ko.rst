.. _`PyPI mirrors and caches`:

================================
Package index mirrors and caches
================================

:Page Status: Incomplete
:Last Reviewed: 2014-12-24

.. contents:: Contents
   :local:


PyPI 미러링 또는 캐싱은 로컬 패키지 설치 속도를 높이고 오프라인 작업을 허용하며, 기업 방화벽과 관련된 문제나 단순한 전반적인 인터넷 문제를 처리하는데 사용 될 수 있다.

여기에는 세 가지 옵션을 사용할 수 있다:

1. pip은 로컬 캐싱 옵션을 제공한다.
2. devpi는 잠재적으로 많은 사용자 또는 컴퓨터에서 공유되는 higher-level 캐싱 옵션을 제공한다.
3. bandersnatch는 모든 PyPI :term:`패키지 <Distribution Package>` 의 완전한 로컬 미러를 제공한다.


Caching with pip
----------------

pip는 다음과 같은 :term:`패키지 <Distribution Package>` 의 로컬에 캐시 된 복사본을 사용하여 설치 속도를 높이는 여러 가지 기능을 제공한다:

1. 프로젝트의 모든 requirement를 다운로드하고 PyPI로 가지 않고 다운로드 된 파일에 대해 pip를 사용하는 `빠른 로컬 설치 <https://pip.pypa.io/en/latest/user_guide.html#fast-local-installs>`_.
2. `pip wheel <https://pip.readthedocs.io/en/latest/reference/pip_wheel.html>`_ 을 이용하여 requirement에 들어가는 설치 파일들을 pre-build하는 위의 변형::

    $ pip wheel --wheel-dir=/tmp/wheelhouse SomeProject
    $ pip install --no-index --find-links=/tmp/wheelhouse SomeProject


Caching with devpi
------------------

devpi는 노트북이나 항상 억세스 가능한 컴퓨터에서 실행하는 캐싱 프록시 서버이다. `devpi
documentation for getting started`__ 를 참조.

__ http://doc.devpi.net/latest/quickstart-pypimirror.html


Complete mirror with bandersnatch
----------------------------------

bandersnatch는 모든 PyPI :term:`패키지 <Distribution Package>` 의 완전한 로컬 미러를 설정한다. 단, 외부 호스팅되는 패키지는 미러링 되지 않는다. `bandersnatch documentation for getting that going`__ 참조.

__ https://bitbucket.org/pypa/bandersnatch/overview

devpi의 장점은 PyPI에 호스팅되는 :term:`패키지 <Distribution Package>` 만 캐시하는 bandersnatch와는 다르게 PyPI 외부의 :term:`패키지 <Distribution Package>` 도 포함하는 미러를 생성한다.
