============================
네임스페이스 패키지 패키징
============================

네임스페이스 패키지는 여러 개의 단일 용어 `<Import Package>` 와 구분된 용어 `<Distribution Package>`  내에서 서브 패키지와 모듈을 나눌 수 있게 해준다. (모호함을 피하기 위해 *distribution* 을 사용함). 예를 들면, 다음의 패키지 구조를 가진다면:

.. code-block:: text
    
    mynamespace/
        __init__.py
        subpackage_a/
            __init__.py
            ...
        subpackage_b/
            __init__.py
            ...
        module_b.py
    setup.py

그리고 아래의 코드를 통해 패키지를 사용한다::

    from mynamespace import subpackage_a
    from mynamespace import subpackage_b

그리고나서 서브패키지를 두 개의 distribution으로 나눌 수 있다.:

.. code-block:: text
    
    mynamespace-subpackage-a/
        setup.py
        mynamespace/
            subpackage_a/
                __init__.py

    mynamespace-subpackage-b/
        setup.py
        mynamespace/
            subpackage_b/
                __init__.py
            module_b.py

각각의 서브패키지는 구분되어서 설치되고 사용되고 버젼화 된다.

네임스페이스 패키지는 약간 관련된 패키지의 큰 규모의 컬렉션에 유용할 수 있다.
(such as a large corpus of client libraries for multiple products from
a single company). 그러나, 네임스페이스 패키지는 몇 가지 주의사항이 있으며 모든 경우에 적절하지는 않다. 간단한 대안은 ``import mynamespcae_subpackage_a`` 같은 접두어를 사용하는 것이다. ( 임포트 object를 짧게 유지하기 위해 심지어 ``import mynamespace_subpackage_a as subpackage_a`` 를 사용할 수도 있다.)


네임스페이스 패키지 만들기
============================

네임스페이스 패키지를 만드는 방법은 3가지가 있다.:

#. `native namespace packages`_ 를 사용. 네임스페이스 패키지의 이 타입은 :pep:`420`    에 정의되어있고 파이썬3.3 이후 버전에서 사용 가능하다. 만약 네임스페이스의 패키지   가 파이썬 3을 지원을 필요로 하고 ``pip`` 를 통해 설치해야 한다면 이 방법이 추천된    다.

#. `pkgutil-style namespace packages`_ 를 사용하는 방법이다. 파이썬2 또는 3을 지원해   야하고 ``pip`` 와 ``python setup.py install`` 을 통해 설치를 한다면 이 방법이 추    천된다.

#. `pkg_resources-style namespace packages`_ 를 사용하는 방법이다. 패키지에 대한 호    환성이 필요하거나 패키지가 zip-safe를 필요로 하는 경우 이 방법이 추천된다.

.. warning:: native 네임스페이스 패키지와 pkgutil-stype namespace 가 주로 호환이 되는 반면에, pkg_resources-style namespcae는 다른 방법과 호환이 되지 않는다. 동일한 네임스페이스에 패키지를 자공하는 다른 배포판에서는 다른 방법을 사용하는 것이 바람직하지 않다.

Native namespace packages 
--------------------------------

파이썬3.3은 :pep:`420` 으로부터 **implicit** 한 네임스페이스 패키지를 더한다. native 네임스페이스 패키지를 만들기 위해 요구되는 것은 단지 네임스페이스 패키지 디렉토리로부터 ``__init__.py`` 를 생략하는 것이다. 파일 구조 예제 : 

.. code-block:: text

    setup.py
    mynamespace/
        # No __init__.py here.
        subpackage_a/
            # Sub-packages have __init__.py.
            __init__.py
            module.py

네임스페이스 패키지를 사용하는 모든 배포판이 ``__init__.py`` 를 생략하거나 pkgutil-style의 ``__init__.py`` 를 사용하는 것은 매우 중요하다.  그렇지 않으면, 네임스페이스 로직에 문제가 생길 것이고 다른 서브패키지 또한 임포트할 수 없게된다. 

``mynamespace`` 는 ``__init__.py`` 를 포함하지 않기 때문에, :func:`setuptools.find_packages` 는 서브 패키지를 찾지 못할 것이다. 그래서 명시적으로 ``setup.py`` 에 모든 패키지 리스트가 있어야 한다. 예를 들면 :

.. code-block:: python

    from setuptools import setup

    setup(
        name='mynamespace-subpackage-a',
        ...
        packages=['mynamespace.subpackage_a']
    )

두 개의 native 네임스페이스 패키지의 완전한 작동 예제는 `native namespace package example project`_ 에서 찾을 수 있다. 

.. _native namespace package example project:
    https://github.com/pypa/sample-namespace-packages/tree/master/native

.. note:: navtive와 pkgutil-style 네임스페이스 패키지는 주로 호환이 되기 때문에, 단지 파이썬3을 지원하는 배포판에서 native 네임스페이스 패키지를 사용할 수 있고 파이선2와 3에 대한 지원을 필요로 하는 배포판에서는 pkgutil-style 네임스페이스 패키지를 사용할 수 있다.

pkgutil-style namespace packages
----------------------------------

파이썬 2.3은 `pkgutil`_ 모듈과 `extend_path`_ 함수를 도입했다. 이는 파이썬2.3+와 파이썬3 모두에 호환을 필요로 하는 네임스페이스 패키지를 선언하는데 사용되어 질 수 있다. 이는 가장 높은 레벨의 호환성을 위해 추천되는 접근 방법이다.

pkgutil-style 네임스페이스 패키지를 만들기 위해, 네임스페이스 패키지를 위한 ``__init__.py`` 파일을 제공할 필요가 있다.:


.. code-block:: text

    setup.py
    mynamespace/
        __init__.py  # Namespace package __init__.py
        subpackage_a/
            __init__.py  # Sub-package __init__.py
            module.py

네임스페이스 패키지를 위한 ``__init__.py`` 파일은 단지 다음에 오는 것을 포함해야한다.:

.. code-block:: python

    __path__ = __import__('pkgutil').extend_path(__path__, __name__)

네임스페이스 패키지를 사용하는 **모든** 배포판은 동일한 ``__init__.py`` 를 포함해야한다. 그렇지 않으면, 네임스페이스 로직에 문제가 발생할 수 있고 다른 서브패키지를 임포트 할 수 없을 것이다. ``__init__.py`` 의 추가적인 코드에도 접근이 불가능하다. 

두 개의 pkgutil-style 네임스페이스 패키지의 완전한 작동 예제는 `pkgutil namespace example project`_. 에서 찾을 수 있다.

.. _pkgutil: https://docs.python.org/3/library/pkgutil.html
.. _extend_path:
    https://docs.python.org/3/library/pkgutil.html#pkgutil.extend_path
.. _pkgutil namespace example project:
    https://github.com/pypa/sample-namespace-packages/tree/master/pkgutil


pkg_resources-style namespace packages
----------------------------------------

`Setuptools`_ 는 :func:`~setuptools.setup` 에 `pkg_resources.declare_namespace`_ 함수와 ``namespace_packages`` argument를 제공한다. 이들을 함께 사용하여 네임스페이스 패키지를 선언할 수 있다. 이 방법은 더 이상 추천되지 않지만, 대부분의 기존 네임스페이스 패키지에 널리 사용된다. 이 방법을 사용하는 기존 네임스페이스 패키지 내에서 새로운 배포판을 만든다면, 다른 방법은 상호 호환이 안되고 기존 패키지를 마이그레이션 하는데 바람직하지 않으므로 현재 방법을 계속해서 사용하는 것이 추천된다.

pkg resources-style 네임스페이스 패키지를 만들기 위해, 네임스페이스 패키지에 ``__init__.py`` 파일을 제공할 필요가 있다.


.. code-block:: text

    setup.py
    mynamespace/
        __init__.py  # Namespace package __init__.py
        subpackage_a/
            __init__.py  # Sub-package __init__.py
            module.py

네임스페이스 패키지를 위한 ``__init__.py`` 파일은 다음에 오는 것을 필요로 한다.:

.. code-block:: python

    __import__('pkg_resources').declare_namespace(__name__)

네임스페이스 패키지를 사용하는 모든 배포판은 동일한 ``__init__.py`` 를 포함해야한다.그렇지 않으면, 네임스페이스 로직에 문제가 발생할 수 있고 다른 서브패키지를 임포트 할 수 없을 것이다. ``__init__.py`` 의 추가적인 코드에도 접근이 불가능하다.

.. note:: 일부 이전의 추천은 다음의 네임스페이스 패키지를 추천한다. 
   ``__init__.py`` :

    .. code-block:: python

        try:
            __import__('pkg_resources').declare_namespace(__name__)
        except ImportError:
            __path__ = __import__('pkgutil').extend_path(__path__, __name__)

   
    이 배후의 아이디어는 드문 경우이다. setuptools를 사용할 수 없는 패키지가 pkgutil-stype 패키지로 대체 되는 경우이다. pkgutil과 pkg_resources-style 네임스페이스 패키지는 상호 호환이 되지 않기 때문에 이는 바람직하지않다. setuptools의 존재가 문제가 된다면 패키지는 명시적으로 ``install_requires`` 를 통해 setuptools에 의존한다.

마지막으로, 모든 배포판은 ``setup.py`` 에 있는 :func:`~setuptools.setup` 에 ``namespace_packages`` argument를 제공해야한다. 예를 들면 :


.. code-block:: python

    from setuptools import find_packages, setup

    setup(
        name='mynamespace-subpackage-a',
        ...
        packages=find_packages()
        namespace_packages=['mynamespace']
    )

두 개의 pkg_resources-style 네임스페이스 패키지의 완전한 작동 예제는 `pkg_resources namespace example project`_ 에서 찾을 수 있다.


.. _setuptools: https://setuptools.readthedocs.io
.. _pkg_resources.declare_namespace:
    https://setuptools.readthedocs.io/en/latest/setuptools.html#namespace-packages
.. _pkg_resources namespace example project:
    https://github.com/pypa/sample-namespace-packages/tree/master/pkg_resources
