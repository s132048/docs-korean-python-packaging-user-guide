.. _`Wheel vs Egg`:

============
Wheel vs Egg
============

:term:`Wheel` 과 :term:`Egg` 는 패키징 포맷으로, 테스트나 제작 워크플로우에서
비용이 많이 드는(costly) 컴파일이나 빌드를 요구하지 않는 설치 아티팩트(artifact)를
필요로 하는 사용 케이스(case) 지원을 목적으로 한다.

:term:`Egg` 포맷은 2004년 :ref:`setuptools`\ 에 의해 도입되었고,
:term:`Wheel` 포맷은 :pep:`427`\ 에 의해 2012년에 도입되었다.

:term:`Wheel`\ 은 현재 파이썬용 패키지 :term:`built <Built Distribution>`\ 과
:term:`binary <Binary Distribution>`\ 의 표준으로 간주되고 있다.

아래는 :term:`Wheel`\ 과 :term:`Egg`\ 의 중요한 차이점을 설명한 것이다.


* :term:`Wheel`\ 는 :pep:`official PEP <427>`\ 를 따르고 :term:`Egg`\ 은
  따르지 않는다.

* :term:`Wheel` \ 는 :term:`distribution <Distribution Package>` 포맷이다, 즉
  패키징 포맷이다. [1]_ :term:`Egg`\ 는 배포 포맷이며 동시에 런타임 설치 포맷이기도
  하다 (압축되어 있는 경우), 그리고 임포터블(importable) 하도록 디자인 되었다.

* :term:`Wheel` 아카이브는 .pyc 파일을 포함하지 않는다. 따라서 배포판이 파이썬
  파일만 포함할 때 (즉, 컴파일된 확장판이 없을 때), 그리고 파이썬 2, 3과 호환 가능할
  때 wheel이 :term:`sdist <Source Distribution (or "sdist")>`\ 와 비슷하게
  "범용(universal)"이 될 수 있다.

* :term:`Wheel`\ 은 :pep:`PEP376-compliant <376>` ``.dist-info``
  디렉토리를 사용하고 Egg는 ``.egg-info``\ 를 사용했다.

* :term:`Wheel`\ 는 :pep:`richer file naming convention <425>`\ 를 따른다.
  단일 wheel 아카이브는 여러 파이썬 언어 버전에 대한 호환성과
  임플리멘테이션(implementaions), ABIs, 시스템 아키텍쳐를 표시한다.

* :term:`Wheel`\ 는 버전관리 된다. 모든 wheel 파일은 해당 wheel 버전의 내역과
  패키징한 임플리멘테이션을 포함하고 있다.

* :term:`Wheel`\ 는 `sysconfig path type
  <http://docs.python.org/2/library/sysconfig.html#installation-paths>`_\ 에
  의해 내부적으로 체계화되어 있어서 다른 포맷으로 변환하기 쉽다.

----

.. [1] 경우에 따라서는 사정에 따라 wheel은 임포터블한 런타임 포맷으로 사용될 수 있다.
       하지만 :pep:`현재 공식적으로 지원되는 것은 아니다
       <427#is-it-possible-to-import-python-code-directly-from-a-wheel-file>`.
