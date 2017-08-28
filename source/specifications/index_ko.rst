
.. _specifications:

===================
PyPA Specifications
===================

이 문서는 현재 Python Packaging Authority에 의해 관리돠고 있는
interoperability specification 목록이다.

Package distribution metadata
#############################

Core metadata
=============

현재의 core metadata file format version 1.2은 :pep:`345` 에 명시되어 있다.

하지만 위의 PEP의 version specifier와 environment marker 섹션은 아래에 설명 된 대로
대체되었다. 또한 metadata 파일은 다음 내용의 추가 필드를 허용한다.

Provides-Extra (multiple use)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

선택적 기능의 이름을 포함하는 string. 유효한 Python identifier이여야 한다..
선택적 기능이 요청되었는지 여부에 따라 dependency을 조건부로 만드는 데 사용할 수 있다.

예::

    Provides-Extra: pdf
    Requires-Dist: reportlab; extra == 'pdf'

두 번째 distribution에서는 대괄호 안에 선택적 종속성이 필요하며, 쉼표 (,)로 구분하여
여러 기능을 요청할 수 있다. Requirement는 요청 된 각 기능에 대해 평가되고 distribution
의 requirement 모음에 추가된다.

예::

    Requires-Dist: beaglevote[pdf]
    Requires-Dist: libexample[test, doc]

`test`와 `doc`이라는 두 가지 기능 이름은 자동 테스트를 실행하고 문서를 생성하는 데 필요한
dependency를 표시하기 위해 예약되어 있다.

``Requires-Dist:`` 에서 참조하지 않더라도 ``Provides-Extra:`` 에서 지정하는 것도 허용된다.

Description-Content-Type
~~~~~~~~~~~~~~~~~~~~~~~~

도구가 설명을 렌더링 할 수 있도록, distribution 설명에 사용 된 markup syntax가 있는 경우를
나타내는 string이다.

역사적으로, PyPI에서는 plain text와 `reStructuredText
(reST) <http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html>`_ 형식의
설명을 지원했었고, reST를 HTML로 렌더링 할 수 있었다. 하지만 distribution의 제작자가
설명을 `Markdown <https://daringfireball.net/projects/markdown/>`_ (`RFC 7763
<https://tools.ietf.org/html/rfc7763>`_) 으로 작성하는 것도 흔한 편이다. 이는 많은
코드 호스팅 사이트들이 Markdown README를 렌더링 하므로 제작자가 설명 파일을 재사용
하기 때문이다. PyPI는 이 포맷을 인식하지 못했으므로 이를 제대로 렌더링 하지 못했었다.
이 필드는 distribution 저자가 그들의 설명 format을 지정함으로써 PyPI와 다른 도구들이
Markdown과 다른 format들을 렌더링 할 수 있게 해준다.

이 필드의 형식은 HTTP의 ``Content-Type`` 헤더와 동일하다. (즉,
`RFC 1341 <https://www.w3.org/Protocols/rfc1341/4_Content-Type.html>`_)
간단히 말해서, 이것은 ``type/subtype`` 부분을 가지고 있으며, 선택적으로 여러 개의 parameter를
가질 수 있다 :

형식::

    Description-Content-Type: <type>/<subtype>; charset=<charset>[; <param_name>=<param value> ...]

``type/subtype`` 부분은 몇 가지 허용되는 value를 가진다.

- ``text/plain``
- ``text/x-rst``
- ``text/markdown``

``charset`` parameter는 description의 character 인코딩을 지정하는데 사용 될 수 있다.
허용되는 유일한 value는 ``UTF-8`` 이다. 만약 생략된다면 ``UTF-8`` 으로 가정된다.

다른 parameter는 특정 subtype에만 쓰일 수도 있다. 예를들어, ``markdown`` subtype에는
현재 쓰이는 Markdown의 종류를 지정하는 선택적인 ``variant`` parameter가 있다.
만약 지정되지 않는다면 이는 default로 ``CommonMark`` 가 된다. 현재 인식되는
유일한 value는 다음과 같다:

- ``CommonMark`` for `CommonMark
  <https://tools.ietf.org/html/rfc7764#section-3.5>`_

예::

    Description-Content-Type: text/plain; charset=UTF-8

예::

    Description-Content-Type: text/x-rst; charset=UTF-8

예::

    Description-Content-Type: text/markdown; charset=UTF-8; variant=CommonMark

예::

    Description-Content-Type: text/markdown

만약 ``Description-Content-Type`` 이 지정되지 않으면, 응용 프로그램은 그것을
``text/x-rst; charset=UTF-8`` 로 렌더링 하는 것을 시도하고, 만약 유효한 rst가 아니라면
``text/plain``로 되돌려야 한다.

만약 ``Description-Content-Type`` 이 인식되지 않는 value인 경우, 가정되는 type은
``text/plain`` 이다. (하지만 PyPI는 아마도 인식 할 수 없는 value가 있다면 reject 할 것이다)

만약 ``Description-Content-Type`` 이 ``text/markdown`` 이고 ``variant`` 가
지정되지 않거나 인식되지 않는 value라면 가정되는 ``variant`` 는 ``CommonMark`` 이다.

따라서 위의 마지막 예제에서 ``charset`` 는 ``UTF-8`` 로 가정되고 ``variant`` 는
``CommonMark`` 로 가정된다. 따라서 앞그 이전의 예와 동일하다.


Version Specifiers
==================

Version 번호 부여 requirement와 version 사이의 비교를 지정하는 semantic은 :pep:`440`
에 정의되어 있다.

이 PEP의 version specifier 섹션은 pep:`345` 의 version specifier 섹션을 대체한다.

Dependency Specifiers
=====================

다른 component에 대한 dependency를 선언하는데 사용되는 dependency specifier 형식은
:pep:`508` 에 정의되어 있다.

이 PEP의 environment marker 섹션은 :pep:`345` 의 environment marker 섹션을 대체한다.

Declaring Build System Dependencies
===================================

`pyproject.toml` 은 빌드 시스템과 독립적인 파일 포맷으로, :pep:`518` 에 정의되어 있다.
이는 project의 빌드 시스템을 성공적으로 실행하기 위해 인스톨 되어야 하는 Python 레벨에서의
dependency를 선언하기 위해 제공 될 수 있다.

Source Distribution Format
==========================

Source distribution format(``sdist``)은 현재 공식적으로 정의되어 있지 않다.
대신, ``setup.py sdist`` command를 실행 할 때 standard library의 ``disutils`` module의
동작에 의해 암시적으로 정의된다.

Binary Distribution Format
==========================

Binary distribution format(``wheel``)은 :pep:`427` 에 정의되어 있다.

Platform Compatibility Tags
===========================

``wheel`` distribution을 위해 사용되는 platform compatibility tagging model은 
:pep:`425` 에 정의되어 있다.

위의 PEP에 정의된 scheme으로는 Linux wheel 파일들과 \*nix wheel 파일들의 public
distribution에는 적합하지 않으므로, ``manylinux1`` 태그를 정의하기 위해 :pep:`513` 가
생성되었다.

Recording Installed Distributions
=================================

설치된 package와 내용을 기록하는데 사용되는 형식은 :pep:`376` 에 정의되어 있다.

해당 PEP의 ``dist-info`` 디렉토리와 ``RECORD`` 파일 형식 만이 현재 default packaging
toolchain에 구현되어 있다.


Package index interfaces
########################

Simple repository API
=====================

사용 가능한 package 버전을 쿼리하고 index 서버에서 package를 가져오기 위한 현재 인터페이스는
:pep:`503` 에 정의되어 있다.
