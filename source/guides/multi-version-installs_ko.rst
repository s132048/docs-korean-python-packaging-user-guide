
.. _`Multi-version Installs`:

멀티 버전 설치
======================


easy_install을 사용하면 단일 환경에 동일한 프로젝트의 다른 버전들의 동시 설치를 할 수 있다. 이러한 단일 환경은 런타임( ``pkg_resources`` 를 사용함)에 적절한 버전의 프로젝트를 ``require``  해야하는 여러 프로그램에 의해 공유되어진다.  

다양한 사용 케이스에 대해, 가상 환경 주소는 ``require`` directive의 복잡성 없이 이러한 요구를 해결한다. 그러나 같은 환경에서의 동시 설치의 이점은 리눅스 배포판의 파이썬 같은 멀티플 애플리케이션에 의해 공유되는 환경에서  작동한다는 것이다.  

동시 설치에 기초한 ``pkg_resources`` 의 주된 한계는 ``pkg_resources`` 를 임포트 하자마자, 이미 sys.path에서 사용 가능했던 모든 *default* 버전을 잠근다는 것이다. ``setuptools`` 가 작성한 커맨드 라인 스크립트는 실행할 엔트로 포인트를 찾기 위해 ``pkg_resources`` 를 사용하기 때문에, 문제의 원인이 될 수 있다.
예를 들면 만약 애플리케이션이 표준 ``sys.path`` 에서 사용 가능한 것의 non-default 버전을 필요로 한다면, 이는 ``nose`` 를 통해 호출된 test 또는 ``gunicorn`` 에 의해 호출된 WSGI 애플리케이션을 ``require`` 를 할 수 없다는 것을 의미한다.
sys.path - 기본 애플리케이션을 위한 스크랩트 래퍼는 기본적으로 이용 가능한 버전에서 잠길 것이므로, 뒤에 따라 오는 코드에서 ``require`` 호출은 잘못된 버전과의 충돌에 의해 실패한다.


이것은 처음에 ``pkg_resources`` 를 임포트 하기 전에, ``__main__.__require__`` 에서 모든 종속성을 설정함으로서 작동할 수 있다. 그러나 그 접근이 영향을 받은 툴들의 표준 커맨드 라인의 호출을 사용할 수 없음을 의미한다. 애플리케이션의 메인 엔트리 포인트를 직접적으로 호출하기 위해서는 커스텀 래퍼 스크립트를 작성하거나 ``python -c '<command>'`` 를 사용하는 것이 필요하다.

더 자세히 알고 싶다면  `pkg_resources documentation
<https://setuptools.readthedocs.io/en/latest/pkg_resources.html#workingset-objects>`__
를 참고하면 된다.
