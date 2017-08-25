================================
Creating and discovering plugins
================================

종종 Python application이나 library를 만들 때 **플러그인** 을 통해 사용자에게
customization이나 추가 기능을 제공하기를 바랄 것이다. Python package는 개별적으로
배포 할 수 있으므로 application 또는 library에서 사용 가능한 모든 플러그인을 자동으로 **검색**
할수 있기를 바랄 것이다.

자동 플러그인 검색을 수행하는 데에는 세 가지 주요 접근법이 있다:

#. `Using naming convention`_.
#. `Using namespace packages`_.
#. `Using package metadata`_.


Using naming convention
=======================

Application의 모든 plugin이 동일한 naming 규약을 따르는 경우, :func:`pkgutil.iter_modules`
를 사용하여 naming 규약과 일치하는 모든 top-level module을 검색 할 수 있다.
예를 들어, `Flask`_ 는 naming 규약으로 ``flask_{plugin_name}`` 을 사용한다.
설치된 모든 Flask plugin을 자동으로 검색하려면 다음과 같이 하면 된다:

.. code-block:: python

    import importlib
    import pkgutil

    flask_plugins = {
        name: importlib.import_module(name)
        for finder, name, ispkg
        in pkgutil.iter_modules()
        if name.startswith('flask_')
    }

`Flask-SQLAlchemy`_ 와 `Flask-Talisman`_ plugin이 모두 설치되어 있다면
``flask_plugins`` 는 다음과 같다:

.. code-block:: python

    {
        'flask_sqlachemy': <module: 'flask_sqlalchemy'>,
        'flask_talisman': <module: 'flask_talisman'>,
    }

Plugin에 대한 naming 규약을 사용하면, 당신의 naming 규약에 따르는 모든 패키지에 대해
Python Package Index의 `simple API`_ 를 통해 검색 할 수 ​​있다.

.. _flask: https://flask.pocoo.org
.. _Flask-SQLAlchemy: https://flask-sqlalchemy.pocoo.org/
.. _Flask-Talisman: https://pypi.python.org/pypi/flask-talisman
.. _simple API: https://www.python.org/dev/peps/pep-0503/#specification


Using namespace packages
========================

:doc:`Namespace packages <packaging-namespace-packages>` 는 plugin을 어디에 둘
것인지를 결정하는 규약을 제공하거나 검색을 하는 방법을 제공하는데 사용 될 수 있다. 예를 들어,
sub-package ``myapp.plugins`` 를 namespace package로 만들면 다른
:term:`distribution <Distribution Package>` 은 그 namespace에 module과 package를
제공 할 수 있다. 설치가 끝나면, :func:`pkgutil.iter_modules` 를 사용하여 해당 namespace에
설치된 모든 module과 package를 검색 할 수 있다.

.. code-block:: python

    import importlib
    import pkgutil

    import myapp.plugins

    def iter_namespace(ns_pkg):
        # Specifying the second argument (prefix) to iter_modules makes the
        # returned name an absolute name instead of a relative one. This allows
        # import_module to work without having to do additional modification to
        # the name.
        return pkgutil.iter_modules(ns_pkg.__path__, ns_pkg.__name__ + ".")

    myapp_plugins = {
        name: importlib.import_module(name)
        for finder, name, ispkg
        in iter_namespace(myapp.plugins)
    }

``myapp.plugins.__ path__`` 를 :func:`~ pkgutil.iter_modules` 에 지정하면,
이 namespace 아래에있는 module만 찾는다. 예를 들어, ``myapp.plugin.a`` 와
``myapp.plugin.b`` module을 제공하는 distribution을 설치했다면이 경우
``myapp_plugins`` 는 다음과 같다 :

.. code-block:: python

    {
        'a': <module: 'myapp.plugins.a'>,
        'b': <module: 'myapp.plugins.b'>,
    }

This sample uses a sub-package as the namespace package (``myapp.plugin``), but
it's also possible to use a top-level package for this purpose (such as
``myapp_plugins``). How to pick the namespace to use is a matter of preference,
but it's not recommended to make your project's main top-level package (
``myapp`` in this case) a namespace package for the purpose of plugins, as one
bad plugin could cause the entire namespace to break which would in turn make
your project unimportable. For the "namespace sub-package" approach to work,
the plugin packages must omit the ``__init__.py`` for your top-level package
directory (``myapp`` in this case) and include the namespace-package style
``__init__.py`` in the namespace sub-package directory (``myapp/plugins``).
This also means that plugins will need to explicitly pass a list of packages
to :func:`setup`'s ``packages`` argument instead of using
:func:`setuptools.find_packages`.

.. warning:: Namespace package는 복잡한 기능이며 여러 가지 방법으로 만들 수 있다.
:doc:`packaging-namespace-packages` documentation을 읽고 프로젝트에 대한 plugin에
어떤 접근 방식이 선호되는지 명확하게 기록하는 것이 좋다.

Using package metadata
======================

`Setuptools`_ 는 plugin을 위한 `special support`_ 를 제공한다. ``setup.py`` 안의 :func:`setup`
에 대한 ``entry_points`` argument를 제공함으로써, plugin은 검색을 위해 스스로를
등록 할 수 있다.

예를 들어, ``myapp-plugin-a`` 라는 패키지가 있고 그것의 ``setup.py`` 에
다음이 포함되어 있다면:

.. code-block:: python

    setup(
        ...
        entry_points={'myapp.plugins': 'a = myapp_plugin_a'},
        ...
    )

그러면 :func:`pkg_resources.iter_entry_points` 를 사용하여 등록된 모든 entry point를
검색하고 로딩할 수 있다:

.. code-block:: python

    import pkg_resources

    plugins = {
        entry_point.name: entry_point.load()
        for entry_point
        in pkg_resources.iter_entry_points('myapp.plugins')
    }

이 예에서 ``plugins`` 는 다음과 같다:

.. code-block:: python

    {
        'a': <module: 'myapp_plugin_a'>,
    }

.. note:: ``setup.py`` 의 ``entry_point`` specification은 상당히 유연하고 많은 옵션이 있다.
`entry points`_ 에 대한 전체 섹션을 읽어두는 것이 좋다.

.. _Setuptools: http://setuptools.readthedocs.io
.. _special support:
.. _entry points:
    http://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins
