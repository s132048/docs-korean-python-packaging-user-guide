.. _`Migrating to PyPI.org`:

PyPI.org로 마이그레이션하기 
============================

PyPI.org은 새롭게 다시 쓰여진 PyPI의 버전이고 PyPI는pypi.python.org에 있는 레거시 코드 기반을 대체한다. 그것이 기본값이 되고, 결국에는 PyPI 사용자의 버전은 상호 작용을 할 것으로 예상되므로, 툴과 프로세스가 새로운 위치를 처리하기 위해 업데이트를 필요로 하는 전환 기간이 있을 것이다. 이 섹션은 다른 업무를 위해 새로운 PyPI.org를 마이그레이션 하는 방법을 포함한다.

업로딩
---------

업로딩을 위해 PyPI.org로 마이그레이션을 하는 추천하는 방법은 새로운 버젼의 업로드 툴을 사용하는 것을 보장하는 것이다. PyPI.org를 지원하는 툴은 기본적으로 twine v1.8.0+, setuptools 27+ 또는 파이썬3.4.6+, 3.6+, 2.7.13+에 포함되는 distutils이다.

새로운 버전의 툴의 사용을 보장하는 것과 더불어, 또한 기본 업로드 URL을 오버라이드 하기 위해 툴을 구성하지 말아야한다. 일반적으로 이는 ``~/.pypirc`` 에 위치하는 파일에서 구성된다 이런 파일을 본다면. :

.. code::

    [distutils]
    index-servers =
        pypi

    [pypi]
    repository:https://pypi.python.org/pypi
    username:yourusername
    password:yourpassword


단순히 ``repository`` 로 시작하는 라인을 삭제하고 업로드 툴의 기본 URL 값을 사용할 것이다. 

몇몇의 이유에서 기본적으로 PyPI.org를 사용하는 버전의 툴을 업그레이드 하는 것이 불가능할 것이다. 그리고 나서, ``~/.pypirc`` 와 ``repository:`` 를 포함하는 라인을 수정할 수도 있다. 그러나 대신에 ``https://upload.pypi.org/legacy/`` 를 사용해라. :

.. code::

    [distutils]
    index-servers =
        pypi

    [pypi]
    repository: https://upload.pypi.org/legacy/
    username: your username
    password: your password


패키지 이름과 메타데이터를 등록하기
------------------------------------

첫번째 업로드 이전에 ``setup.py register`` 커맨드를 가진 패키지 네임의 명확한 사전등록은 더 이상 요구되어 지지 않는다. 그리고 지금은 PyPI.org에서 레거시 업로드 API 에뮬레이션에 의해 지원되지 않는다.

따라서 업로드를 위해 PyPI.org를 사용하는 것으로 바꾼 후에 명확한 등록을 시도하는 것은 다음의 에러 메시지를 보여줄 것이다. :: 

    Server response (410): This API is no longer supported, instead simply upload the file.

해결 방법은 등록 스텝을 건너뛰고 직접적으로 업로드 하는 것이다.


TestPyPI 사용하기
-------------------

TestPyPI를 사용한다면, TestPyPI의 새로운 위치를 다루기 위해 ``~/.pypirc`` 를 업데이트 해야한다. 이는 ``https://testpypi.python.org/pypi``
를 ``https://test.pypi.org/legacy/`` 로 대체함으로써 가능하다. 예를 들면:

.. code::

    [distutils]
    index-servers=
        pypi
        testpypi

    [testpypi]
    repository: https://test.pypi.org/legacy
    username: your testpypi username
    password: your testpypi password
