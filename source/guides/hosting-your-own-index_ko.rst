.. _`Hosting your Own Simple Repository`:

=====================================
자신의 simple repository 호스팅하기
=====================================


자신만의 simple repository [1]_ 를 호스팅 하려는 경우, `devpi`_ 와 같은 소프트웨어 패키지를
사용하거나 적절한 디렉토리 구조를 만들고 static file을 제공 할 수있는 웹 서버를 사용하여 autoindex를
생성하면 된다.

두 경우 모두 사용자의 default repository에 없는 repository를 호스팅 할 것이므로, 프로젝트의
설명서를 통해 사용자가 설치 프로그램을 적절히 설정하도록 해야한다. 다음은 pip을 사용하는 예이다::

    pip install --extra-index-url https://python.example.com/ foobar

또한 유효한 HTTPS를 사용하여 repository를 제공하는 것이 **매우 권장된다**. 현재, 사용자 설치시
보안은 모든 repository가 유효한 HTTPS 설정을 사용하는 것에 의존한다.


"Manual" Repository
===================

디렉토리 레이아웃은 상당히 간단하다. 루트 디렉토리 내에서 각 프로젝트에 대한 디렉토리를 만들어야 한다. 이
디렉토리는 PEP 503에 정의된 대로 프로젝트의 정규화 된 이름이어야 한다. 이 디렉토리들 각각에 다운로드
가능한 파일을 하나씩 배치한다. 예를 들어, 프로젝트 "Foo" version 1.0과 2.0, "bar" version
0.1이 있다면 다음과 같은 구조를 가져야 한다::

    .
    ├── bar
    │   └── bar-0.1.tar.gz
    └── foo
        ├── Foo-1.0.tar.gz
        └── Foo-2.0.tar.gz

이 레이아웃을 설정한 후, autoindex가 활성화 된 상태로 루트 디렉토리를 제공하도록 웹 서버를 설정하기만
하면 된다. 예를 들어, `Twisted`_ 에 내장 된 웹 서버를 사용하는 경우,
``twistd -n web --path .`` 를 실행 한 다음 사용자에게 설치 프로그램의 설정에 URL을 추가하도록
지시한다.

----

.. [1] Simple repository의 protocol의 documentation은 PEP 503을 참조.


.. _devpi: http://doc.devpi.net/latest/
.. _Twisted: https://twistedmatrix.com/
