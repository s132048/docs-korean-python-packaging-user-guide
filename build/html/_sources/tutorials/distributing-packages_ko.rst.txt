===================================
프로젝트 패키징과 배포
===================================

이 섹션은 파이썬 프로젝트를 어떻게 구성하고, 패키징하고, 배포하는지에 대한 기초를
다루고 있으며 독자가 :doc:`installing` 페이지의 내용에 익숙하다는 전제 하에서
진행된다.

이 섹션은 파이썬 프로젝트 전반에 대한 모범 사례들을 다루는 것이 목적이 아니다.
예를 들면, 이 문서는 테스트, 도큐먼테이션, 버전 관리를 위한 툴이나 가이드를 추천하지
않는다.

:ref:`setuptools`에 있는 `Building and Distributing Packages
<https://setuptools.readthedocs.io/en/latest/setuptools.html>`_\ 를 참고하면
더 많은 레퍼런스 자료들을 볼 수있다. 하지만 자료에 있는 내용은 최신화 되지 않은
경우가 있다. 내용이 상충하는 경우 Python Packaging User Guide를 따라라.

.. contents:: 목차
   :local:


패키징과 배포를 위한 요구 조건
===========================================

1. 첫째, :ref:`패키지 설치를 위한 요구 조건 <설치_요구조건>`\ 을
   축종하는지 확인하라.

2. "twine" [1]_\ 을 설치하라:

   ::

    pip install twine

   이것은 프로젝트 :term:`배포판(distributions) <Distribution Package>`\ 을
   :term:`PyPI <Python Package Index (PyPI)>`\ 에 업로드 할 때 필요하다.
   (:ref:`아래 <PyPI에 프로젝트 업로드하기>`\ 를 참고하라).


프로젝트 구성하기
========================


초기 파일
-------------

setup.py
~~~~~~~~

가장 중요한 파일은 "setup.py"이며 프로젝트 디렉토리의 루트에 존재한다. 예시는,
`PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\ 에 있는
`setup.py <https://github.com/pypa/sampleproject/blob/master/setup.py>`_\ 를
참고하라.

"setup.py"는 두 가지 주요 기능을 수행한다:

1. 프로젝트의 여러 부분이 구성되어 있는 파일이다. ``setup.py``\ 의 주요 특징은
   전역 ``setup()`` 함수를 포함하고 있다는 것이다. 이 함수에 대한 키워드 인수는
   프로젝트의 구체적인 디테일을 결정한다. 가장 관련이 높은 인수는
   :ref:`아래쪽 섹션 <setup() args>`\ 에 설명되어 있다.

2. 패키징 작업과 관련된 커맨드를 실행 시키기 위한 커맨드라인 인터페이스다. 이용가능한
   커맨드 목록은 ``python setup.py --help-commands``\ 을 실행하면 확인할 수 있다.


setup.cfg
~~~~~~~~~

"setup.cfg"\ 은 ini 파일로 ``setup.py`` 커맨드를 위한 기본 옵션을 포함하고 있다.
예시는 `PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\ 에 있는
`setup.cfg <https://github.com/pypa/sampleproject/blob/master/setup.cfg>`_\ 를
참고하라.


README.rst
~~~~~~~~~~

모든 프로젝트는 프로젝트의 목표를 설명하는 readme 파일을 포함하고 있어야 한다.
일반적인 포맷은 "rst" 확장자를 가진 `reStructuredText
<http://docutils.sourceforge.net/rst.html>`_\ 이며 요구 조건은 아니다.

예시는, `PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\ 에 있는
`README.rst <https://github.com/pypa/sampleproject/blob/master/README.rst>`_\ 를
확인하라.

MANIFEST.in
~~~~~~~~~~~

:file:`MANIFEST.in`\ 는 소스 배포판에 자동적으로 포함되지 않는 추가적인 파일을
패키징 할 필요가 있는 특별한 경우에 필요하다. 기본적으로 포함되는 항목의 리스트는
:ref:`distutils` 도큐먼테이션의 `배포할 파일 지정하기
<https://docs.python.org/3.4/distutils/sourcedist.html#specifying-the-files-to-distribute>`_\ 를
참고하라.

예시는, `PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\ 의
`MANIFEST.in <https://github.com/pypa/sampleproject/blob/master/MANIFEST.in>`_\ 를
참고하라

``MANIFEST.in`` 파일 작성에 대한 보다 자세한 정보는 :ref:`distutils`\ 의
`The MANIFEST.in template
<https://docs.python.org/2/distutils/sourcedist.html#the-manifest-in-template>`_\ 를
참고하라.


.. note:: :file:`MANIFEST.in`\ 는 wheel 같은 바이너리 배포판에는 영향을 주지 않는다.

LICENSE.txt
~~~~~~~~~~~

모든 패키지는 배포 규정에 대해 자세하게 설명한 라이센스 파일을 포함해야 한다.
많은 국가에서 명시적인 라이센스가 없는 패키지는 저작권 소유자를 제외한 다른
사람에 의해 법적으로 배포되거나 사용될 수 없다. 어떤 라이센스를 선택해야 될지
모르겠다면 `GitHub's Choose a License <https://choosealicense.com/>`_\ 를
참고하거나 변호사에게 자문을 구하라.

예시는 `PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\ 에 있는
`LICENSE.txt <https://github.com/pypa/sampleproject/blob/master/LICENSE.txt>`_\ 를
참고하라.

<your package>
~~~~~~~~~~~~~~

필수는 아니지만, 가장 일반적인 방법은 파이썬 모듈과 패키지를 당신의 프로젝트와 동일한
:ref:`name <setup() name>`\ 를 가진 하나의 최상위 패키지 아레에 파이썬 모듈과
패키지를 포함시키는 것이다.

예시는, `PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_\에 포함되어
있는 `sample <https://github.com/pypa/sampleproject/tree/master/sample>`_\ 을
참고하라.


.. _`setup() args`:

setup() args
------------

위에서 언급했다시피 ``setup.py`\ 의 주요 특징은 ``setup()`` 전역 함수를 포함하고
있다는 사실이다. 이 함수에 대한 키워드 인수는 프로젝트의 구체적인 디테일을 결정한다.

가장 관련이 높은 인수는 아래에 설명되어 있다. 제공되는 스니핏(snippet)은
`PyPA 샘플 프로젝트 <https://github.com/pypa/sampleproject>`_ 에 포함되어 있는
`setup.py <https://github.com/pypa/sampleproject/blob/master/setup.py>`_\ 에서
가져온 것이다.


.. _`setup() name`:

name
~~~~

::

  name='sample',

이 인수는 프로젝트의 이름이며 :term:`PyPI <Python Package Index (PyPI)>`\ 에
프로젝트가 어떤 이름으로 리스트될지를 결정한다. :pep:`508`\ 에 따른 유효한 프로젝트
이름을 사용해야 한다:

- ASCII 문자, 숫자, 언더스코어(``_``), 하이픈(``-``), 구두점(``.``)으로만 구성되어
  있어야 하며
- ASCII 문자 또는 숫자로만 시작하고 종료해야 한다.

프로젝트 이름은 대소문자를 구별하지 않으며 임의로 길게 쓰여진 언더스코어, 하이픈,
구두점 등은 모두 같은 것으로 다루어진다. 예를 들어 만약 프로젝트 이름을 ``cool-stuff``\ 로
등록했다면, 사용자들은 아래의 구문을 사용해서 다운로드 하고 의존성을 선언할 수 있다::

    Cool-Stuff
    cool.stuff
    COOL_STUFF
    CoOl__-.-__sTuFF


version
~~~~~~~

::

  version='1.2.0',

이 인수는 프로젝트의 현재 버전이며, 사용자가 최신 버전을 사용하고 있는지, 사용자가 자신의
소프트웨어를 어느 버전으로 테스트 했는지 알려준다.

프로젝트를 퍼블리시하게 되면 각 릴리즈 마다 :term:`PyPI <Python Package Index (PyPI)>`\ 에
나타나게 된다.

사용자에게 호환성 정보를 전달하는 방법에 대한 자세한 정보는
:ref:`Choosing a versioning scheme`\ 을 참고하라.

만약 프로젝트 코드가 버전에 대한 런타임 접근을 필요로 한다면 ``setup.py``\ 와 코드
양쪽 모두에 버전을 남겨두는 것이 가장 간단한 방법이다. 만약 값을 복제하는 것을
원하지 않으면 이것을 처리하는 방법은 몇 가지가 있다.
":ref:`Single sourcing the version`" Advanced Topics 섹션을 참고하라.


description
~~~~~~~~~~~

::

  description='A sample Python project',
  long_description=long_description,

프로젝트에 대한 간략하거나 상세한 설명을 제공하라. 이 값은 프로젝트를 퍼블리시 하면
:term:`PyPI <Python Package Index (PyPI)>`\ 에 나타날 것이다.


url
~~~

::

  url='https://github.com/pypa/sampleproject',


프로젝트에 대한 홈페이지 url을 제공하라.


author
~~~~~~

::

  author='The Python Packaging Authority',
  author_email='pypa-dev@googlegroups.com',

제작자에 대한 정보를 제공하라.


license
~~~~~~~

::

  license='MIT',

사용하고 있는 라이센스 타입을 제공하라.


classifiers
~~~~~~~~~~~

::

  classifiers=[
      # 프로젝트가 어느 단계에 있는가? 일반적인 값은
      #   3 - Alpha
      #   4 - Beta
      #   5 - Production/Stable
      'Development Status :: 3 - Alpha',

      # 어느 독자를 대상으로 만들어진 프로젝트인지 표시하라
      'Intended Audience :: Developers',
      'Topic :: Software Development :: Build Tools',

      # 원하는 라이센스를 선택하라(위쪽의 "license"와 일치해야 한다)
       'License :: OSI Approved :: MIT License',

      # 지원하는 파이썬 버전을 지정하라. 특히, 파이썬2, 파이썬 3 또는 둘 다를
      # 지원하는지 반드시 표기하라.
      'Programming Language :: Python :: 2',
      'Programming Language :: Python :: 2.6',
      'Programming Language :: Python :: 2.7',
      'Programming Language :: Python :: 3',
      'Programming Language :: Python :: 3.2',
      'Programming Language :: Python :: 3.3',
      'Programming Language :: Python :: 3.4',
  ],

프로젝트를 분류하는 classifiers 목록을 제공하라. 전체 리스팅에 관한 정보는
https://pypi.python.org/pypi?%3Aaction=list_classifiers\ 을 참고하라.

classifiers 목록이 프로젝트가 지원하는 파이썬 버전을 알리기 위해 사용되지만 이는
프로젝트를 설치할 때가 아니라 PyPI에서 프로젝트를 검색할 때만 사용된다.
프로젝트가 설치할 수 있는 파이썬 버전을 실제로 제한하려면
:ref:`python_requires` 인수를 사용하라.


keywords
~~~~~~~~

::

  keywords='sample setuptools development',

프로젝트를 설명하는 키워드를 나열하라.


packages
~~~~~~~~

::

  packages=find_packages(exclude=['contrib', 'docs', 'tests*']),


프로젝트에 포함시키 위해서 :term:`packages <Import Package>`\ 를 리스팅해야 한다.
제작자가 직접 리스팅 할 수도 있지만 ``setuptools.find_packages``\ 가 자동적으로
찾아주기도 한다. 설치나 릴리즈 되지 않아야 할 패키지는 ``exclude`` 키워드 인수를 사용해서
제외할 수 있다.


install_requires
~~~~~~~~~~~~~~~~

::

 install_requires=['peppercorn'],

"install_requires"는 프로젝트를 실행하기 위해서 최소한으로 요구되는 의존성을 지정해주기
위해서 반드시 사용되어야 한다. 프로젝트가 :ref:`pip`\ 로 설치 되었을 때, 이것은
의존성을 설치하기 위해 사용되는 내역서로 사용된다.

"install_requires" 사용에 대한 자세한 정보는 :ref:`install_requires vs Requirements files`\ 를
참고하라.


.. _python_requires:

python_requires
~~~~~~~~~~~~~~~

만약 프로젝트가 특정한 파이썬 버전에서만 실행된다면 :pep:`440`\ 를 따르는
버전 지정자 스트링에 맞게 ``python_requires`` 인수를 세팅해서 다른 파이썬
버전에 프로젝트가 설치되는 것을 막을 수 있다. 예를 들어 패키지가 파이썬 3+에서만
실행된다면, 아래와 같이 작성하라::

    python_requires='>=3',

만약 패키지가 파이썬 3.3 이상에서 실행되지만 파이썬 4 버전을 아직 지원하지 않는다면,
아래와 같이 작성하라::

    python_requires='~=3.3',

패키지가 파이썬 2.6, 2.7, 그리고 3.3으로 시작하는 모든 파이썬 3 버전을 지원한다면
아래와 같이 작성하라::

    python_requires='>=2.6, !=3.0.*, !=3.1.*, !=3.2.*, <4',

이런 식으로 사용한다.

.. note::

    이 기능에 대한 지원은 비교적 최근에 시작되었다. 프로젝트 소스 배포판과
    wheel은 (:ref:`프로젝트 패키징하기` 참고) ``python_requires`` 인수를
    인식하고 적합한 메타데이터를 생성하기 위해 최소 24.2.0 버전 :ref:`setuptools`\ 을
    사용해서 빌드되어야 한다.


    또한, 9.0.0 버전 이상의 :ref:`pip`\ 만이 ``python_requires`` 메타데이터를
    인식한다. 이전 버전의 pip를 사용하고 있는 사용자는 프로젝트의 ``python_requires``
    값과 상관없는 버전의 파이썬에서 프로젝트를 다운로드 하고 설치할 수 있다.


.. _`Package Data`:

package_data
~~~~~~~~~~~~

::

 package_data={
     'sample': ['package_data.dat'],
 },


종종 추가적인 파일은 :term:`package <Import Package>`\ 에 설치되어야 할 필요가 있다.
이 파일들은 패키지 구현에 밀접하게 연관된 데이터이거나 패키지를 사용하는 프로그래머에게
도움이 되는 도큐먼테이션을 포함한 텍스트 파일이다. 이 파일들을 "package data"라고
한다.

값은 패키지 이름을 상대 경로 이름 리스트에 매핑한 것이며 패키지 안에 복사되어야 한다.
경로는 패키지를 포함하고있는 디렉토리에 따라 해석된다.

더 자세한 정보는 `setuptools docs <https://setuptools.readthedocs.io>`_\ 의
`Including Data Files
<https://setuptools.readthedocs.io/en/latest/setuptools.html#including-data-files>`_
을 참고하라.


.. _`Data Files`:

data_files
~~~~~~~~~~

::

    data_files=[('my_data', ['data/data_file'])],

대부분의 경우 :ref:`Package Data`\ 을 설정하하는 것으로 충분하지만, 일부 경우에는
데이터 파일을 :term:`packages <Import Package>`\ 의 *외부에* 놓아야 하는 경우도 있다.
이 경우 ``data_files`` 디렉티브를 사용하면 된다.

시퀀스에 있는 각각의 (디렉토리, 파일) 짝은 설치 디렉토리와 그곳에 설치되는 파일을
지정한다. 만약 디렉토리가 상대 경로라면, 그것은 설치 접두사(prefix 순수 파이썬
:term:`distributions <Distribution Package>`\ 을 위한 파이썬의 sys.prefix, 확장
모듈을 포함하는 배포판을 위한 sys.exec_prefix))에 따라서 해석된다. 파일에 있는
각 파일의 이름은 프로젝트 소스 배포판의 최상위에 있는 ``setup.py`` 스크립트에 따라서
해석된다.

더 자세한 정보는 `Installing Additional Files
<http://docs.python.org/3.4/distutils/setupscript.html#installing-additional-files>`_
에 있는 distutils 섹션을 참고하라.

.. note::

  :term:`sdist <Source Distribution (or "sdist")>`\ 로 설치할 때
  :ref:`setuptools`\ 는 절대 "data_files" 경로를 허용하고, pip도 절대 경로로
  인식한다. 하지만 :term:`wheel` 배포판으로 설치할 때는 그렇지 않다. Wheel은
  절대 경로를 지원하지 않으며 "site-packages"\ 로 설치한다.
  이에 대한 논의는 `wheel Issue #92 <https://bitbucket.org/pypa/wheel/issue/92>`_
  를 참고하라.


scripts
~~~~~~~

``setup()``\ 이 설치된 사전 제작된 스크립트를 가리키는 `scripts
<http://docs.python.org/3.4/distutils/setupscript.html#installing-scripts>`_
키워드를 지원하지만, 교차 플랫폼의 호환성을 달성하기 위해 추천하는 방법은
:ref:`console_scripts` 엔트리 포인트를 사용하는 것이다 (아래를 참고하라).


entry_points
~~~~~~~~~~~~

::

  entry_points={
    ...
  },


당신의 프로젝트 혹은 당신이 의존하는 다른 프로젝트에 의해 정의될 수 있는 명명된
엔프리 포인트에 대해 당신 프로젝트가 제공하는 플러그인을 지정하려면 이 키워드를
사용하라.

더 자세한 정보는 :ref:`setuptools`\ 에 있는 `Dynamic Discovery of Services and
Plugins
<https://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins>`_
섹션을 참고하라.

가장 흔하게 사용되는 엔트리 포인트는 "console_scripts"다 (아래를 참고하라).

.. _`console_scripts`:

console_scripts
***************

::

  entry_points={
      'console_scripts': [
          'sample=sample:main',
      ],
  },

당신의 스크립트 인터페이스를 등록하려면 "console_script" `entry points
<https://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins>`_\ 를
사용하라. 그러면 툴체인(toolchain)으로 인터페이스를 실제 스크립트로 바꾸는 작업을
처리하게 할 수 있다 [2]_.  이 스크립트는 :term:`distribution <Distribution
Package>`\ 를 설치하는 동안에 생성될 것이다.

더 자세한 정보는 `setuptools docs <https://setuptools.readthedocs.io>`_ 에 있는
`Automatic Script Creation
<https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation>`_\ 를
참고하라.

.. _`Choosing a versioning scheme`:

Choosing a versioning scheme
----------------------------

Standards compliance for interoperability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다른 파이썬 프로젝트는 특정한 프로젝트에서 필요로 하는 다른 버전 관리 스킴(scheme)을
사용하지만, ``pip``\ 와 ``setuptools``\ 같은 라이브러리나 툴에서 지원받기 위해서는
모든 프로젝트는 :pep:`440`\ 에서 명시된 유연한 :pep:`public version scheme
<440#public-version-identifiers>`\ 을 따를 필요가 있다.

아래는 공공 스킴을 따르는 버전 숫자 예시다::

  1.2.0.dev1  # Development release
  1.2.0a1     # Alpha Release
  1.2.0b1     # Beta Release
  1.2.0rc1    # Release Candidate
  1.2.0       # Final Release
  1.2.0.post1 # Post Release
  15.10       # Date based release
  23          # Serial release

버전 넘버링에 대한 히스토리의 변형을 수용하기 위해 :pep:`440`\ 는
변형된 구문을 표준화된 형태로 대응시켜 놓은 :pep:`version
normalisation <440#normalization>`\ 에 대한 포좔적인 기술을 정의해 놓았다 .

스킴 선택
~~~~~~~~~~~~~~

시맨틱 버저닝 (선호됨)
*******************************

새로운 프로젝트의 경우 권장되는 버전 관리 스킴은 `Semantic Versioning
<http://semver.org>`_\ 을 바탕으로 한다. 하지만 사전 릴리즈 처리와 메타데이터 빌드에
대해서는 다른 접근방식을 채택했다.

시멘틱 버저닝의 본질은 제작자가 증가시켜가는 3단계 MAJOR.MINOR.MAINTENANCE 숫자 스킴이다:

1. 호환되지 않는 API 변화가 있를 경우 MAJOR 버전을,
2. 하위 호환 방식에서 기능이 추가됐을 때 MINOR 버전을,
3. 하위 호환 버그를 고쳤을 때 MAINTENANCE 버전을 증가시킨다.

이 방식을 채택하면 프로젝트 제작자는 사용자들의 :pep:`"compatible release"
<440#compatible-release>` 지정자 사용을 허용하게 된다.
``name ~= X.Y``\ 는 최소 X.Y 릴리즈가 필요하지만 MAJOR 버전이 일치하는
후속 릴리즈도 허용한다.

시멘틱 버전 관리를 채택한 파이썬 프로젝트는
`Semantic Versioning 2.0.0 specification <http://semver.org>`_\ 의 1-8 조항에
따라 유지되어야 한다.

Date based versioning
*********************

시멘틱 버전 관리는 정기 날짜 기반 케이던스(cadence)와 기능 제거 이전의 많은 릴리즈에
경고를 제공하는 디프리케이션(deprecation) 처리 같은 프로젝트에는 적합하지 않은 선택이
될 수 있다.

날짜 기반 버전 관리의 핵심 장점은 특정 릴리즈의 기본 기능이 얼마나 오래 됬는지
버전 숫자를 통해서 쉽게 알 수 있다는 점이다.

날짜 기반 프로젝트의 버전 숫자는 전형적으로 YEAR.MONTH 형태를 취한다. (예,
``12.04``, ``15.10``).

Serial versioning
*****************

이것은 가장 간단한 버저닝 스킴이며 매 릴리즈마다 증가하는 숫자 하나로 구성되어 있다.

순차 버전 관리는 개발자로서 관리하기가 매우 쉽지만 사용자로서는 쫓아가기가 매우 어렵다.
왜냐하면 순차 버전 숫자는 API 하위 호환성에 관해 정보를 제공하지 않거나 아주 적은
정보만 전달하기 때문이다.

Hybrid schemes
**************

위 스킴들을 조합해서 사용하는 것도 가능하다. 예를 들어, 프로젝트는 날짜 기반 버저닝과
순차 버저닝을 결합시켜 릴리즈의 대략적인 세대는 전달하지만 해당 년도 내에 있는 릴리즈
케이던스 명시하지 않는 YEAR.SERIAL 숫자 스킴 만들 수도 있다.

Pre-release versioning
~~~~~~~~~~~~~~~~~~~~~~

기본 버전 관리 스킴과 상관없이 최종 릴리즈를 위한 사전 릴리즈는 아래와 같이 퍼블리시 될
수 있다:

* 0 또는 이상의 dev 릴리즈 (뒤에 ".devN" 표기)
* 0 또는 이상의 alpha 릴리즈 (뒤에 ".aN" 표기)
* 0 또는 이상의 beta 릴리즈 (뒤에 ".bN" 표기)
* 0 또는 이상의 release candidates (뒤에 ".rcN" 표기)

``pip``\ 와 다른 최신 파이썬 패키지 인스톨러는 설치될 의존성 버전을 결정할 때
기본적으로 사전 릴리즈는 무시한다.


Local version identifiers
~~~~~~~~~~~~~~~~~~~~~~~~~

공공 버전 식별자는 :term:`PyPI <Python Package Index (PyPI)>`\ 를 통해서 배포판을
지원하도록 디자인 되어 있다. 파이썬의 소프트웨어 배포 툴은
:pep:`로컬 버전 식별자 <440#local-version-identifiers>`\ 의 견해를 지지한다.
이 식별자는 공개용이 아니닌 로컬 개발 빌드나 재배포자에 의해 관리되는 릴리즈의 수정된 변형인지를
식별하는 데 사용할 수 있다.

로컬 버전 식별자는 ``<public version identifier>+<local version label>``\ 형식을
취한다.
예시::

   1.2.0.dev1+hg.5.b11e5e6f0b0b  # 1.2.0.dev1 릴리즈 이후 5th VCS 커밋
   1.2.1+fedora.4                # downstream Fedora 패치가 적용된 패키지


Working in "Development Mode"
=============================

필수는 아니지만, 작업을 할 때 프로젝트를 "editable" 모드나 "develop" 모드에서
로컬에 설치하는 것이 일반적이다. 이것은 프로젝트를 프로젝트 형태에서 편집하고
설치할 수 있게 해준다.

당신이 프로젝트 디렉토리의 루트에 있다고 가정하고, 실행해보자:

::

 pip install -e .


다소 암호같기는 하지만 ``-e``\ 는 ``--editable``\ 을 축약한 것이고  ``.``\ 는
현재 작업 디렉토리를 의미한다. 그래서 합치면 현재 디렉토리(당신의 프로젝트)에
편집모드로 설치하라는 뜻이다. 이것은 또한 "install_requires"\ 로 선언된 의존성과
"console_scripts"\ 로 선언된 스크립트를 설치할 것이다.

당신의 의존성 일부를 편집 모드로 설치하는 것을 원할 수도 있다. 예를 들어,
당신의 프로젝트가 "foo"와 "bar"을 요구한다고 가정하고 당신은 "bar"을 편집 모드로
VCS에서 설치하고 싶다고 하자. 그러면 당신은 요구 조건 파일을 아래와 같이 작성할 수 있다::

  -e .
  -e git+https://somerepo/bar.git#egg=bar

첫 번째 줄은 당신의 프로젝트와 모든 의존성을 설치하라는 의미이고
두 번째 줄은 "bar" 의존성을 오버라이드(override) "bar" 의존성을 PyPI가 아니라
vcs로 수행하라는 의미이다.

그러나 만약 편집 모드로 로컬 디렉토리에 "bar"를 설치하고 싶다면, 요구 조건 파일은
아래와 같이 보이며 로컬 경로를 파일의 상단에 적어주어야 한다.

  -e /path/to/project/bar
  -e .

반면에 의존성은 요구 조건 파일의 설치 순서 때문에 PyPI에서 수행될 것이다.
요청 파일에 대한 자세한 정보는 pip 문서의 :ref:`요구 조건 파일
<pip:Requirements Files>` 섹션을 참고하라. vcs 설치에 관한 정보는,
pip 문서의 :ref:`VCS Support <pip:VCS Support>` 섹션을 참고하라.

마지막으로 의존성을 전혀 설치하고 싶지 않으면 아래와 같이 실행하면 된다::

   pip install -e . --no-deps


더 자세한 정보는, `setuptools docs <https://setuptools.readthedocs.io>`_\ 의
`Development Mode
<https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode>`_
섹션을 참고하라.

.. _`프로젝트 패키징하기`:

프로젝트 패키징하기
======================

:term:`PyPI <Python Package Index (PyPI)>` 같은 :term:`Package Index`로부터
당신의 패키지가 설치 가능하게 하려면 :term:`Distribution
<Distribution Package>` (":term:`Package <Distribution Package>`")를
생성해야 할 필요가 있을 것이다.



소스 배포판
--------------------

최소한, :term:`Source Distribution <Source Distribution (or "sdist")>`\ 을
생성해야 한다:

::

 python setup.py sdist


"source distribution"는 빌드되지 않은 상태이며 (즉, :term:`Built Distribution`\ 이 아니다),
pip에 의해 설치될 때 빌드 단계를 요구한다. 배포판이 순수 파이썬(즉, 확장 라이브러리를
포함하지 않음)일 경우에도 여전히 ``setup.py``\ 로부터 설치 메타데이터를 만드는 빌드
단계를 포함하고 있다.


Wheels
------

또한 당신은 프로젝트를 위해서 wheel을 생성해야 한다.
Wheel은 "빌드" 과정을 없이 설치될 수 있는 :term:`built package
<Built Distribution>`\ 다. Wheel 설치는 소스 배포판에서 설치하는 것 보다
최종 사용자로 설치하는 것이 훨씬 빠르다.

프로젝트가 순수 파이썬이고 기본적으로 파이썬 2와 3을 지원한다면, 당신은
:ref:`*유니버셜 Wheel* (아래 섹션 참고) <유니버셜 wheels>`\ 을 생성하게 될
것이다.

만약 프로젝트가 순수 파이썬이 아니고 파이썬 2와 3 둘 중 하나만 지원한다면,
당신은 :ref:`"순수 파이썬 Wheel" (아래 섹션 참고) <순수 파이썬 wheels>`\ 을
생성하게 될 것이다.

만약 패키지가 컴파일된 확장 라이브러리를 포함하고 있다면 당신은
:ref:`*플랫폼 wheel* (see section below) <플랫폼 wheels>`\ 라고 불리는 것을
생성하게 될 것이다.

프로젝트를 위해 wheel을 빌드하기 전에 ```wheel`` 패키지를 설치해야 한다:

.. code-block:: text

  pip install wheel


.. _`유니버셜 wheels`:

유니버셜 Wheels
~~~~~~~~~~~~~~~~

*유니버셜 Wheels*\ 은 (컴파일된 확장 라이브러리를 포함하지 않은) 순수 파이썬 wheel이고
파이썬 2와 3을 지원한다. :ref:`pip`\ 로 아무 위치에나 설치할 수 있다.

Wheel 빌드하기:

.. code-block:: text

  python setup.py bdist_wheel --universal

당신은 "setup.cfg" (`sampleproject/setup.cfg 참고
<https://github.com/pypa/sampleproject/blob/master/setup.cfg>`_)\ 에
``--universal`` 플래그를 영구적으로 설정할 수 있다.


.. code-block:: text

  [bdist_wheel]
  universal=1

만약 아래 상황인 경우 ``--universal`` 세팅만 사용하라:

1. 프로젝트가 변경 없이 파이썬 2와 3에서 실행되는 경우(즉, 2to3을 필요로 하지
   않는 경우).
2. 프로젝트에 C 확장 파일이 없는 경우.

``bdist_wheel``\ 은 현재 당신이 부적절하게 세팅을 사용해도 경고를 해주지 않는다는
점을 주의하라.

만약 당신의 프로젝트가 선택적인 C 확장 파일을 가지고 있으면, universal wheel을
퍼블리시하지 않을 것을 권장한다. 왜냐하면 pip는 소스 설치보다 wheel을 선호하고
확장 파일을 빌드할 가능성을 없애버리기 때문이다.


.. _`순수 파이썬 wheels`:

순수 파이썬 wheels
~~~~~~~~~~~~~~~~~~

"universal" 하지 않는 *순수 파이썬 wheel*\ 은 (컴파일된 확장 파일을 포함하지 않는
) 순수 파이썬 wheel이지만, 기본적으로 파이썬 2와 3 모두를 지원하지는 않는다.

wheel 빌드하기 :

::

 python setup.py bdist_wheel


`bdist_wheel`\ 는 코드가 순수 파이썬인지를 감지해낼 것이고, wheel을 빌드하기 위해
사용했던 동일한 메이저 버전(파이썬 2 또는 3)을 사용하는 어떠한 파이썬 설치에도 사용할
수 있는 명명된 wheel을 빌드할 것이다. Wheel 파일 작명에 대한 자세한 내용은
:pep:`425`\ 를 참고하라.

만약 당신의 코드가 다른 코드를 써서 (예,
`"2to3" <https://docs.python.org/2/library/2to3.html>`_\ 을 사용) 파이썬 2와 3을
같이 지원한다면, ``setup.py bdist_wheel``\ 를 한 번은 파이썬 2로 한 번은 파이썬 3으로
두 번 실행시킬 수 있다. 이 작업은 각 버전에 맞는 wheel을 생성할 것이다.



.. _`플랫폼 wheels`:

플랫폼 wheels
~~~~~~~~~~~~~~~

*플랫폼 wheels* 는 일반적으로 컴파일된 확장 파일을 포함하는 것 때문에 리눅스나
맥OS, 윈도우 같은 특정 플랫폼에 한정된 wheel이다.

wheel 빌드하기:

::

 python setup.py bdist_wheel


`bdist_wheel`\ 은 코드가 순수 파이썬인지 감지할 것이고, 해당하는 플랫폼에서만
사용할수 있는 이름으로 명명된 wheel을 빌드할 것이다. Wheel 파일 작명에 대한 자세한 내용은
:pep:`425`\ 를 참고하라.

.. note::

  :term:`PyPI <Python Package Index (PyPI)>`\ 는 현재 윈도우즈, 맥OS, 다중 distro
  ``manylinux1`` ABI를 위한 플랫폼 wheel 업로드를 지원한다..
  ABI에 대한 세부사항은 :pep:`513`\ 를 참고하라.


.. _`PyPI에 프로젝트 업로드하기`:

PyPI에 프로젝트 업로드하기
==============================

배포판을 생성하기 위해 커맨드를 실행할 때 새로운 디렉토리 ``dist/``\ 가
프로젝트의 루트 디렉토리 안에 생성된다. 그곳에서 업로드할 배포 파일을 찾을 수 있다.

.. note:: 메인 PyPI 저장소에 릴리즈 하기 전에, 반 정기적으로 정리되는
  `PyPI test site <https://testpypi.python.org/pypi>`_\ 로 트레이닝 하는 것을
  선호하게 될 것이다. 테스트 사이트를 사용하기 위해 어떻게 설정해야 하는지는
  `이 문서  <https://wiki.python.org/moin/TestPyPI>`_ 를 참고하라.

.. warning:: 다른 자료에서 ``python setup.py register``\ 와 ``python setup.py upload``\ 를
  사용하는 레퍼런스를 봤을 수 있다. 이 패키지를 업로드하고 등록하는 이 방법들은 **굉장히
  권장되지 않는다** 왜냐하면 그것은 일반 텍스트 HTTP 또는 파이썬 버전에 대한 증명되지
  않은 HTTPS 연결을 사용해서 당신의 사용자 이름과 비밀번호가 전송중에 가로채질 수 있기
  때문이다.

계정 생성하기
-----------------

첫 번째로, 당신은 :term:`PyPI <Python Package Index (PyPI)>` 사용자 계정이 필요하다.
당신은 `PyPI 웹사이트의 서식을 사용해 <https://pypi.python.org/pypi?%3Aaction=register_form>`_
계정을 생성할 수 있다.

.. Note:: 업로드 할 때 사용자 이름과 비밀번호를 입력하는 것을 피하고 싶다면,
  사용자 이름과 비밀번호가 있는 ``~/.pypirc`` 파일을 만들면 된다:

  .. code-block:: text

    [pypi]
    username = <username>
    password = <password>

  **비밀번호가 일반 텍스트로 저장된다는 점을 주의하라**

.. _register-your-project:

배포판 업로드하기
-------------------------

일단 계정이 있으면 :ref:`twine`\ 을 이용해 배포판을 :term:`PyPI <Python Package Index (PyPI)>`\ 에
업로드 할 수 있다. 만약 새로운 프로젝트에 대해 처음 업로드 하는 경우라면, twine이
프로젝트를 등록하는 것을 처리해 줄 것이다.

.. code-block:: text

    twine upload dist/*


.. note:: Twine는 gpg를 사용해 당신이 배포 파일에 사전 날인하게 할 수 있다:

  .. code-block:: text

      gpg --detach-sign -a dist/package-1.0.1.tar.gz

  그리고 gpg로 생성된 .asc 파일을 커맨드라인 invocation에 전달할 수 있다:

  .. code-block:: text

      twine upload dist/package-1.0.1.tar.gz package-1.0.1.tar.gz.asc

  이렇게 하면 *당신이* ``gpg`` 커맨드를 직접 실행하는 유일한 사람이 될 것이기 때문에
  gps 패스프레이즈를 gpg에 입력하는 것만으로 안전을 보장 받게 해준다.


----

.. [1] 당신의 플랫폼에 따라서, 이것은 루트나 관리자 권한을 요구할 수도 있다.
       :ref:`pip`\ 는 현재 `사용자 인스톨을 기본 작동으로 만듦으로써
       <https://github.com/pypa/pip/issues/1668>`_ 이것을 바꾸는 것을 고려하고
       있다.


.. [2] 특히, "console_script" 처리 방법은 ``.exe`` 파일을 윈도우즈에 생성하며,
       이는 OS special-case ``.exe`` 파일 때문에 필요하다. ``PATHEXT``\ 과
       :pep:`Python Launcher for Windows <397>` 같은 스크립트 실행 기능은
       스크립트를 전부는 아니지만 많은 케이스에서 쓰일 수 있게 해준다.
