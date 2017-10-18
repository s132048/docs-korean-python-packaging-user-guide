.. _`Supporting multiple Python versions`:

===================================
다중 파이썬 버전 지원
===================================

:Page Status: Incomplete
:Last Reviewed: 2014-12-24

.. contents:: Contents
   :local:


::

  FIXME

  Useful projects/resources to reference:

  - DONE six
  - DONE python-future (http://python-future.org)
  - tox
  - DONE Travis and Shining Panda CI (Shining Panda no longer available)
  - DONE Appveyor
  - DONE Ned Batchelder's "What's in Which Python"
    - http://nedbatchelder.com/blog/201310/whats_in_which_python_3.html
      - http://nedbatchelder.com/blog/201109/whats_in_which_python.html
  - Lennart Regebro's "Porting to Python 3"
  - Greg Hewgill's script to identify the minimum version of Python
    required to run a particular script:
    https://github.com/ghewgill/pyqver
  - the Python 3 porting how to in the main docs
  - cross reference to the stable ABI discussion
    in the binary extensions topic (once that exists)
  - mention version classifiers for distribution metadata

파이썬 패키지를 만드는데 요구되는 작업에 더해서, 패키지는 파이썬의 다른 버전에서도 이용 가능하게 만들어져야한다. 다른 파이썬 버젼은 다른 표준 라이브러리 패키지를 포함할 수 도 있고 파이썬 2.x 와 3.x 사이의 변화가 언어 syntax에 포함 되었을 수도 있다.

모든 테스트는 수동으로 수행되기 때문에, 패키지가 시간이 많이 걸릴 수 있는 모든 파이썬 버전에서 정확하게 작동하는지를 확인해야한다.  운이 좋게도, 이를 처리하는 몇몇의 도구가 있고 여기서 이러한 도구들을 간단하게 알아볼 것이다.

자동화 테스트 및 지속적인 통합
--------------------------------------------

자동 테스트를 위해 여러 호스트 서비스가 이용 가능하다. 이러한 서비스는 일반적으로 소스 코드 저장소(예 `Github <https://github.com>`_ 또는 `Bitbucket <https://bitbucket.org>`_ )를 모니터링하고 커밋이 될 때마다 프로젝트의 테스트 스위트를 실행한다.

이러한 서비스들은 또한 *Python의 여러 버전* 에 있는 프로젝트의 테스트 스위트를 실행할 수 있는 기능을 제공하여 개발자가 직접 테스트를 할 필요없이 코드가 잘 작동하는지에 대한 빠른 피드백을 준다.


위키피디아는 지속적인 통합 시스템에서 광범위한 `비교
<http://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software>`_
를 가진다.  결합해서 사용되는 두 개의 호스트 서비스는 리눅스, 맥, 윈도우에서 자동화 테스트 기능을 제공한다.:

  - `Travis CI <https://travis-ci.org>`_ 는 리눅스와 맥OS 환경을 제공한다. 이 글을 작성하고 있는 시점에서 리눅스 환경은 Ubuntu 12.04 LTS Server Edition 64 bit 이고 맥 OS는 10.9.2 이다.
  - `Appveyor <http://www.appveyor.com>`_  윈도우 환경
    (Windows Server 2012)을 제공한다.

::

    TODO Either link to or provide example .yml files for these two
    services.

    TODO How do we keep the Travis Linux and macOS versions up-to-date in this
    document?

`Travis CI`_ 와 Appveyor_ 모두 테스트를 위한 명령에 대한 상세 기술서로써 `YAML <http://www.yaml.org>`_ 포맷의 파일을 요구한다.
테스트가 실패하면, 구체적인 상황에 대한 출력 로그가 검사 되어질 수 있다.

단일 소스 전략을 사용하여 파이썬2와 파이썬3 모두에 사용할 수 있는 프로젝트의 경우 많은 옵션을 가지고 있다. 


단일 소스 파이썬 패키지를 위한 도구
----------------------------------------

`six <http://pythonhosted.org/six/>`_ 는 파이썬2와 3 사이의 차이를 래핑하기 위해 벤자민 피터슨에 의해 개발되어졌다. six_ 패키지는 널리 사용되어지고 파이썬2와 3 모두에서 사용될 수 있는 단일 소스 파이썬 모듈을 작성할 수 있는 신뢰성 있는 방법으로 여겨진다. 
six_ 모듈은 파이썬 2.5 버전부터 사용 가능하다. 
`modernize <https://pypi.python.org/pypi/modernize>`_ 라고 불리는 툴은 아르민 로나쳐에의해 개발되어졌고 six_ 에 의해 제공되어진 코드 변형을 자동으로 적용하는데 사용될 수 있다.
six_ 와 유사하게 `python-future <http://python-future.org/overview.html>`_ 는 파이썬2와 3의 소스 코드 사이에 호환성 레이어를 제공하는 패키지이다.
그러나 six_ 와는 달리, 이 패키지는 파이썬2와 3 사이의 상호 운용성에 두 파이썬 버전 중 하나와 일치하는 언어의 sysntax를 제공하는 것이 목적이다. : 

  - a Python 2 (by syntax) module in a Python 3 project.
  - a Python 3 (by syntax) module in a *Python 2* project.

양방향성 때문에, python-future_ 는 파이썬2 패키지를 파이썬3 syntax로 모듈 단위로 변환시키는 통로를 제공한다. 그러나 six_ 와는 반대로 python-future_ 는 파이썬 2.6으로만 지원된다. six_ 에 대해 modernize_ 하는 것과 유사하게, python-future_ 는 ``futurize``와 ``pasteurize`` 라는 두 개의 스크립트가 있다. 이는 파이썬2 모듈 또는 파이썬 3 모듈에 각각 적용되어 질 수 있다. 

six_ 또는 python-future_ 의 사용은 추가적인 런타임 종속성을 패키지에 추가시킨다. python-future_ 에서는 ``futurize`` 스크립트가 호출되는데 이는 파이썬2.6+가 파이썬3으로 순방향 호환성을 제공한 변경에 대해서만 적용하기 위해서 ``--stage1`` 옵션을 사용하여 호출된다. 
남아있는 다른 호환성 문제는 수동 변경이 요구된다. 


파이썬에는 어떤 것들이 있나?
------------------------------

Ned Batchelder는
`파이썬 2 <http://nedbatchelder.com/blog/201109/whats_in_which_python.html>`__ 용과 
`파이썬 3 <http://nedbatchelder.com/blog/201310/whats_in_which_python_3.html>`__ 용 각각의 파이썬 릴리즈의 변경 사항에 대한 목록을 제공한다. 이 목록은 파이썬 버전 간의 변경 사항이 패키지에 영향을 줄지 여부를 확인하는데 사용할 수 있다.

::

    TODO These lists should be reproduced here (with permission).

    TODO The py3 list should be updated to include 3.4
