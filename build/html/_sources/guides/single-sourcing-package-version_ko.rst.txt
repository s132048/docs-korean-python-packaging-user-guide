.. _`Single sourcing the version`:

===================================
패키지 버전 단일 소싱
===================================

프로젝트의 버전 넘버에 대한 단일 소스를 유지하는 많은 기술이 있다.:

#.  ``setup.py`` 파일을 읽고 정규식으로 버전을 파싱해라. 예(
     `pip setup.py <https://github.com/pypa/pip/blob/1.5.6/setup.py#L33>`_ 로부터)::

        def read(*names, **kwargs):
            with io.open(
                os.path.join(os.path.dirname(__file__), *names),
                encoding=kwargs.get("encoding", "utf8")
            ) as fp:
                return fp.read()

        def find_version(*file_paths):
            version_file = read(*file_paths)
            version_match = re.search(r"^__version__ = ['\"]([^'\"]*)['\"]",
                                      version_file, re.M)
            if version_match:
                return version_match.group(1)
            raise RuntimeError("Unable to find version string.")

        setup(
           ...
           version=find_version("package", "__init__.py")
           ...
        )

    .. note::

        이 기술은 정규표현식의 복잡성을 다룸에 있어 단점이 있다.        


#.  업데이트된 위치를 관리하거나 위치에서 사용할 수 있는 API를 제공해주는 외부 빌드 도구를 사용해라.

    특정한 순서 없이, 사용할 수 있는 몇 가지 도구가 있고 반드시 완성해야 하는 것은 아니다. :
    `bumpversion <https://pypi.python.org/pypi/bumpversion>`_,
    `changes <https://pypi.python.org/pypi/changes>`_, `zest.releaser <https://pypi.python.org/pypi/zest.releaser>`_.


#.  프로젝트 전용 모듈에서 ``__version__`` 전역 변수에 값을 설정해라. (예 ``version.py``), 그리고 나서, ``setup.py`` 를 읽고 값을 변수로 ``exec`` 해라. 

    ``execfile`` 사용하기 :

    ::

        execfile('...sample/version.py')
        # now we have a `__version__` variable
        # later on we use: __version__

    ``exec`` 사용하기 :

    ::

        version = {}
        with open("...sample/version.py") as fp:
            exec(fp.read(), version)
        # later on we use: version['__version__']

    이 기술을 이용한 예제: `warehouse <https://github.com/pypa/warehouse/blob/master/warehouse/__about__.py>`_.

#.  값을 간단한 ``VERSION`` 텍스트 파일에 위치 시키고, setup.py와 프로젝트 코드 모두    를 읽게 한다.

  
    ::

        with open(os.path.join(mypackage_root_dir, 'VERSION')) as version_file:
            version = version_file.read().strip()

    이 기술의 장점은 파이썬에만 국한되지 않는다는 것이다. 다른 도구도 버전을 읽을 수    있다.
    

    .. warning::

        이 접근을 통해 ``VERSION`` 파일이 모든 소스와 바이너리 배포판에 포함되어 있         는지 확인해야한다. (예 ``MANIFEST.in`` 에  ``include VERSION``  를 추가해라.).

#.  ``setup.py`` 에 값을 설정하고 프로젝트 코드가 ``pkg_resources`` API를 사용하게 만든다. 

    ::

        import pkg_resources
        assert pkg_resources.get_distribution('pip').version == '1.2.0'

    ``pkg_resources`` API는 단지 설치 메타데이터에 무엇이 있는지만 알고 있다는 것을 명심해라. 설치 메타데이터는 반드시 현재 임포트된 코드가 아니어도 된다.
  


#.  ``sample/__init__.py`` 에 있는 ``__version__`` 에 값을 설정해라. 그리고 ``setup.py`` 에 ``sample`` 을 임포트해라.

    ::

        import sample
        setup(
            ...
            version=sample.__version__
            ...
        )

    비록 이 기술이 일반적이라도, sample/__init__.py 가 ``install_requires`` 종속성으로부터 패키지를 임포트 한다면, 이것은 setup.py가 실행될 때 아직 설치되지 않을 가능성이 높다. 


#. 코드 대신 버전 제어 시스템(Git, Mercurial 등)의 태그에 버전 번호를 저장하고 `setuptools_scm <https://pypi.python.org/pypi/setuptools_scm>`_ 을 사용하여 버전 번호를 자동으로 추출한다.
