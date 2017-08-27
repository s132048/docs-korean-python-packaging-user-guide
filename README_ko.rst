Python Packaging User Guide
===========================

http://packaging.python.org

"Python Packaging User Guide" (PyPUG)는 현재의 도구를 사용하여 Python에서 distribution을
package화하고 설치하는 방법에 대한 권위있는 자료를 목표로 한다.

Python packaging의 개발을 따르려면 `Python
Packaging Authority <https://www.pypa.io>`_ 을 참조.


Code of Conduct
---------------

Python Packaging User Guide 프로젝트의 코드베이스, 이슈 트래커, 대화방, 메일링 리스트에서
활동하려는 모든 사람들은 `PyPA Code of Conduct`_ (행동강령)을 따를 것을 요구한다.


History
-------

이 가이드는 “Hitchhiker's Guide to Packaging” 에서 2013년 3월에 fork되었다.


How to build this guide
-----------------------

이 가이드를 로컬에 구축하려면 다음이 필요하다:

1. `Nox <https://nox.readthedocs.io/en/latest/>`_. Nox를 설치하거나 업그레이드 하려면
``pip`` 을 사용하면 된다::

      pip install --upgrade nox-automation

2. Python 3.6. 우리의 빌드 스크립트는 Python 3.6에서만 작동하도록 설계되었다.
Python 3.6을 운영체제에 설치하려면 `Hitchhiker's Guide to Python installation instructions
<http://docs.python-guide.org/en/latest/starting/installation/>`__ 참조.

Building the Guide
++++++++++++++++++

가이드를 빌드하려면 소스 폴더에 다음 bash 명령을 실행한다::

  nox -s build

프로세스가 완료되면 ``./build/html`` 디렉토리에서 HTML output을 찾을 수 있다.
``index.html`` 파일을 열면 웹 브라우저에서 가이드를 볼 수 있다. 하지만 http 서버를 사용하여
가이드를 제공하는 것이 권장된다.

Serving the guide using a local HTTP server
+++++++++++++++++++++++++++++++++++++++++++

다음 명령을 사용하여 HTTP 서버를 통해 가이드를 빌드하고 제공 할 수 있다::

  nox -s preview

이 가이드는 http://localhost:8000을 통해 볼 수 있다.

License
-------

The Python Packaging User Guide is licensed under a Creative Commons
Attribution-ShareAlike license: http://creativecommons.org/licenses/by-sa/3.0 .


.. _PyPA Code of Conduct: https://www.pypa.io/en/latest/code-of-conduct/
