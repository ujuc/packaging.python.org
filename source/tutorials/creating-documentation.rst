.. _creating-documentation:

======================
문서 작성
======================

이 세션에서는 `Sphinx`_\를 사용하여 문서를 만들고 `Read The Docs`_\에서 문서를 무료로 호스팅하는 
방법에 대한 기본 사항을 다룹니다.

.. _Sphinx: http://sphinx-doc.org/
.. _Read The Docs: https://readthedocs.org/

Sphinx 설치
-----------------
``pip``\를 사용해 Sphinx를 설치합니다:

.. code-block:: bash

	pip install -U sphinx

다른 설치 방법은 Sphinx에서 작성된 `설치 가이드`_\를 참조하십시오.

.. _설치 가이드: http://www.sphinx-doc.org/en/master/usage/installation.html

Sphinx 시작하기
---------------------------

문서를 저장할 프로젝트 안에 ``docs`` 디렉토리를 만듭니다:

.. code-block:: bash

	cd /path/to/project
	mkdir docs

``docs`` 디렉토리에서 ``spinx-quickstart``\를 실행합니다:

.. code-block:: bash

	cd docs
	sphinx-quickstart

소스 디렉토리를 설정하고, 몇 가지 기본 설정을 안내하며, ``index.rst`` 파일과 ``conf.py`` 파일을 생성합니다.

``index.rst``\에서 프로젝트에 대한 정보를 추가하고 빌드 할 수 있습니다:

.. code-block:: bash

	make html

빌드 프로세스에 대한 자세한 내용은 Read The Docs에서 `가이드`_\를 참조하십시오.

.. _가이드: https://docs.readthedocs.io/en/latest/intro/import-guide.html

다른 소스
-------------

Sphinx와 reStructuredText를 사용하는 방법에 대한 더 자세한 내용은 Hitchhiker's Guide to Python에 
있는 `문서 튜토리얼`_\을 참조하십시오.

.. _문서 튜토리얼: https://docs.python-guide.org/writing/documentation/




