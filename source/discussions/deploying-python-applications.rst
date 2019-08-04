
=============================
파이썬 응용 프로그램 배포
=============================

:Page Status: 불완전함 (Incomplete)
:Last Reviewed: 2014-11-11

.. contents:: Contents
   :local:


개요
========


여러 하드웨어 플랫폼 지원
--------------------------------------

::

  FIXME

  Meaning: x86, x64, ARM, others?

  For Python-only distributions, it *should* be straightforward to deploy on all
  platforms where Python can run.

  For distributions with binary extensions, deployment is major headache.  Not only
  must the extensions be built on all the combinations of operating system and
  hardware platform, but they must also be tested, preferably on continuous
  integration platforms.  The issues are similar to the "multiple Python
  versions" section above, not sure whether this should be a separate section.
  Even on Windows x64, both the 32 bit and 64 bit versions of Python enjoy
  significant usage.



OS 패키징과 설치 프로그램
=========================

::

  FIXME

  - Building rpm/debs for projects
  - Building rpms/debs for whole virtualenvs
  - Building macOS installers for Python projects
  - Building Android APKs with Kivy+P4A or P4A & Buildozer

Windows
-------

::

  FIXME

  - Building Windows installers for Python projects

Pynsist
^^^^^^^

`Pynsist <https://pypi.org/project/pynsist>`__\는 파이썬 프로그램을 파이썬 인터프리터와
함께 번들로 묶어 NSIS 기반의 단일 설치 프로그램으로 만드는 툴입니다. 대부분의 경우, 패키징은 사용자가
파이썬 인터프리터 버전을 선택하고 프로그램 종속성을 선언하도록 되어있습니다. 이 툴은 Windows 용
특정 파이썬 인터프리터를 다운받고, 단일 Windows용 설치 프로그램에서 모든 종속성을 패키지화 합니다.

설치 프로그램은 패키지 시스템과 독립적으로 사용할 수 있는 파이썬 인터프리터를 사용자 시스템에 설치하거나
업데이트 합니다. 프로그램 자체는 설치 프로그램이 시작 메뉴에 추가하여 바로가기에서 시작할 수 있습니다. 
프로그램을 삭제할 경우, 사용자가 설치해둔 파이썬에 문제가 발생하지 않습니다.

pynsist의 가장 큰 장점은 Windows 패키지가 Linux에서 빌드 될 수 있다는 점입니다. 
`documentation <https://pynsist.readthedocs.io>`__\에는 다른 종류 프로그램 (콘솔, GUI)에
대한 몇 가지 예제가 있습니다. MIT 라이센스를 따릅니다.

응용 프로그램 번들
===================

::

  FIXME

  - py2exe/py2app/PEX
  - wheels kinda/sorta


구성 관리
========================

::

  FIXME

  puppet
  salt
  chef
  ansible
  fabric
