.. _`install_requires vs Requirements files`:

======================================
install_requires vs Requirements files
======================================

.. contents:: Contents
   :local:


install_requires
----------------

``install_requires``\ 는 프로젝트가 제대로 돌아가기 위해서 **최소한으로**
필요로 하는 것을 지정해주기 위해 사용되어야 하는 :ref:`setuptools` ``setup.py``
키워드이다. 프로젝트가 :ref:`pip`\ 에 의해 설치될 때 프로젝트의 의존성(dependencies)를
설치하기 위해 사용되는 열거 항목(specifiaction)이다.

예를 들어 만약 프로젝트가 A와 B를 요구한다면 당신의  ``install_requires`` 는 아래와
같을 것이다:

::

 install_requires=[
    'A',
    'B'
 ]

추가적으로 버전의 상한이나 하한을 표시해주는 것이 좋다.

예를 들어, 당신의 프로젝트가 최소한 v1 'A'와 v2 'B'를 요구 한다면 아래와 같이
작성해야 한다:

::

 install_requires=[
    'A>=1',
    'B>=2'
 ]

프로젝트 A가 시멘틱(semantic) 버저닝(versioning)을 따르고, A의 v2가 호환성이
깨진 것을 나타내므로 v2 허용하지 않아야 한다:

::

 install_requires=[
    'A>=1,<2',
    'B>=2'
 ]

``install_requires``\ 을 사용해서 의존성을 특정한 버전이나 특정한 하위 버전
(당신의 의존성의 의존성)에 고정시키는 것은 권장되지 않는다. 이것은 매우 제한적이어서
사용자가 의존성 업그레이드의 이점을 얻는 데에 방해가 된다.

마지막으로 ``install_requires``\ 는 "추상적인" 요구사항의 목록이라는 점을 이해하는
것은 중요하다. 즉 의존성이 해결되는 위치(색인 또는 소스)를 정해주지 않은 이름과 버전
제한에 불과하다. "구체적으로" 지정되는 위치는 :ref:`pip` 옵션을 사용해 설치하는
때에 결정된다. [1]_


Requirements files
------------------

:ref:`Requirements Files <pip:Requirements Files>`\ 는 간단하게 설명하자면
파일에 위치한 :ref:`pip:pip install` 인수의 목록이다.

``install_requires``\ 가 단일 프로젝트에 대한 의존성을 정의하는 반면에,
:ref:`Requirements Files <pip:Requirements Files>`\ 는 완전한 파이선 환경에 대한
요구사항을 정의할 때 사용된다.

``install_requires`` 요구사항은 최소으로 적지만 requirements files는 완전한 환경의
:ref:`repeatable installations <pip:Repeatability>`\ 를 아카이빙할 목적으로
특정한 버전들로 이루어진 방대한 리스트를 포함하고 있다.

``install_requires`` 요구사항은 "추상적"이지만, 즉 특별한 색인과 연결되어 있지 않지만
requirements files는 요구사항을 "구체적으로" 만들어주는 pip 옵션 ``--index-url`` 또는
``--find-links`` 등을 포함한다, 즉 특정한 색인과 패키지 디렉토리와 연동되어 있다. [1]_

``install_requires`` 메타 데이터는 설치될 때 pip에 의해 자동적으로 분석되지만,
requirements files는 그렇지 않고, 사용자가 ``pip install -r``\ 을 사용해서
특별히 설치할 때에만 사용된다.

----

.. [1] "추상적" vs "구체적" 요구사항에 대한 추가적 정보는 아래를 참고하라,
       https://caremad.io/2013/07/setup-vs-requirement/.
