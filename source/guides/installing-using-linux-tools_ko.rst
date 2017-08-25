.. _`Installing pip/setuptools/wheel with Linux Package Managers`:

===========================================================
Installing pip/setuptools/wheel with Linux Package Managers
===========================================================

:Page Status: Incomplete
:Last Reviewed: 2015-09-17


이 section에서는 Linux package manager를 사용하여 :ref:`pip`, :ref:`setuptools`,
:ref:`wheel` 를 설치하는 법을 다룬다.

`Python.org <https://www.python.org>`_ 에서 다운로드 한 Python을 사용하고 있다면
이 section은 적용되지 않는다. 대신 :ref:`installing_requirements` section을 참조한다.

특정 Linux 배포판에서 지원되는 :ref:`pip`, :ref:`setuptools`, :ref:`wheel`
의 version은 일반적으로 구식이며 업데이트는 기능 업데이트 보다는 보안상의 이유로만 이루어 진다. 다만,
특정 배포판의 경우 최신 버전을 지원하도록 repository가 있는 경우도 있다. 우리가 알고 있는
repository는 아래에 설명한다.

또한 배포판 자체 표준에 대한 보안 및 정상화를 위해 패치를 적용하는 것은 다소 일반적이다.
경우에 따라 패치되지 않은 원래 버전과 다른 버그 또는 예기치 않은 동작이 발생할 수 있다.
이것이 만약에 알려지면 아래에 기록 할 것이다.


Fedora
~~~~~~

* Fedora 21:

  * Python 2::

      sudo yum upgrade python-setuptools
      sudo yum install python-pip python-wheel

  * Python 3: ``sudo yum install python3 python3-wheel``

* Fedora 22:

  * Python 2::

      sudo dnf upgrade python-setuptools
      sudo dnf install python-pip python-wheel

  * Python 3: ``sudo dnf install python3 python3-wheel``


최신 버전의 Python 2 전용 pip, setuptools, wheel을 얻으려면,
`Copr Repo instructions <https://fedorahosted.org/copr/wiki/HowToEnableRepo>`__ 를 사용하여
`PyPA Copr Repo <https://copr.fedoraproject.org/coprs/pypa/pypa/>` 를 활성화 시킨후
다음을 실행한다::

  sudo yum|dnf upgrade python-setuptools
  sudo yum|dnf install python-pip python-wheel


CentOS/RHEL
~~~~~~~~~~~

CentOS와 RHEL는 :ref:`setuptools` 가 기본적으로 설치되나,
:ref:`pip`, :ref:`wheel` 을 코어 repository에서 제공하지 않는다.

시스템 Python에 pip과 wheel을 설치하려면, 다음과 같은 두가지 옵션이 있다:

1. `여기의 설명 <https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F>`__
   을 따라서 `EPEL repository <https://fedoraproject.org/wiki/EPEL>`_ 를 활성화 시킨다.
   EPEL 6과 EPEL7에서는 다음과 같이 pip을 설치할 수 있다::

     sudo yum install python-pip

   EPEL 7 **(EPEL 6은 아님)** 에서 다음과 같이 wheel을 설치 할 수 있다.

     sudo yum install python-wheel

   EPEL은 충돌하지 않는 추가 패키지만을 제공하기 때문에, EPEL은 코어 repository에 있는
   setuptools를 제공하지 않는다.


2. `여기의 설명
   <https://fedorahosted.org/copr/wiki/HowToEnableRepo>`__ [1]_ 을 따라서
   `PyPA Copr Repo <https://copr.fedoraproject.org/coprs/pypa/pypa/>`_ 를 활성화
   시킨다. 다음과 같이 pip과 wheel을 설치 할 수 있다::

     sudo yum install python-pip python-wheel

   setuptools를 추가로 업그레이드하려면 다음을 실행한다::

     sudo yum upgrade python-setuptools


pip, wheel, setuptools를 non-system environment에 yum을 이용해서 병렬로 설치하려면 다음과
같은 두가지 옵션이 있다:


1. "Sofware Collections" 기능을 사용하여 pip, setuptools, wheel이 포함 된
parallel collection을 활성화한다.

   * Redhat의 경우 다음을 참조:
     http://developers.redhat.com/products/softwarecollections/overview/
   * CentOS의 경우 다음을 참조: https://www.softwarecollections.org/en/

   Collection에는 최신 버전이 포함되어 있지 않을 수도 있다는 점에 주의해야 한다.

2. `IUS repository <https://ius.io/GettingStarted/>`_ 를 활성화하고
   `parallel-installable <https://ius.io/SafeRepo/#parallel-installable-package>`_
   Python 중 하나를 pip, setuptools, wheel과 함께 설치 한다.

   예를 들어, CentOS7 또는 RHEL7의 Python 3.4에서는 다음과 같이 한다::

     sudo yum install python34u python34u-wheel


openSUSE
~~~~~~~~

* Python 2::

    sudo zypper install python-pip python-setuptools python-wheel


* Python 3::
 
    sudo zypper install python3-pip python3-setuptools python3-wheel


Debian/Ubuntu
~~~~~~~~~~~~~

::

  sudo apt-get install python-pip

Python 3에서는 "python"을 "python3"로 대체한다.


.. warning::

   최근 Debian/Ubuntu 버전은 `"User Scheme"
   <https://pip.pypa.io/en/stable/user_guide/#user-installs>`_ 을 사용하기 위해 변형된
   pip을 default로 가지고 있다. 이는 작동이 상당히 다르므로 놀랄 수도 있다.


Arch Linux
~~~~~~~~~~

* Python 2::

    sudo pacman -S python2-pip

* Python 3::

    sudo pacman -S python-pip

----

.. [1] 현재 CentOS/RHEL에서 사용할 수 있는 "copr" yum plugin이 없으므로,
       설명 된 대로 repo 파일을 수동으로 배치하는 것이 유일한 옵션이다.
