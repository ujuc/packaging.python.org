.. _`install_requires vs requirements files`:

======================================
install_requires vs requirements files
======================================

.. contents:: Contents
   :local:


install_requires
----------------

``install_requires``\는 :ref:`setuptools` :file:`setup.py` 가 키워드입니다.
프로젝트가 작동하는데 필요한 **최소한**\의 패키지를 일컫습니다. 프로젝트가 :ref:`pip`\를 이용하여 
설치할때, 의존성을 고려하여 설치하기 위해 사용되는 스펙입니다.

예를 들어, 프로젝트가 A와 B가 필요하다면, ``install_requires``\는 다음과 같이 사용합니다:

::

 install_requires=[
    'A',
    'B'
 ]

또한 버전에 대해서 상한과 하한을 나타내는 것을 권장합니다.

예를 들어, 이 프로젝트에서는 'A' 패키지는 v1 이상, 'B' 패키지는 v2 이상이 필요하다는 것을 다음과 같이
나타냅니다:

::

 install_requires=[
    'A>=1',
    'B>=2'
 ]

프로젝트 'A'를 사용하는데 v2에서 호환성이 깨졌으면, 다음과 같이 의미론적 버저닝을 통해 v2를 사용하지
않을 수 있습니다:

::

 install_requires=[
    'A>=1,<2',
    'B>=2'
 ]

``install_requires``\에서 의존성을 특정 버전에 고정하거나 하위 의존성(의존성의 의존성)을 
지정하는 방법은 권장되지 않습니다. 이는 지나치게 제한적이며, 사용자가 의존성 업그레이드의 이점을 
얻지 못하게 됩니다.

마지막으로, ``install_requires``\는 "추상(Abstract)적인" 요구 사항 리스트이며, 의존성이 
어디에서 만족이 될지 (어떤 인덱스나 소스로부터) 결정되지 않는 이름과 버전에 대한 제한 사항임을 
이해하는 것이 중요합니다. 어떻게 "고정적(Concrete)"으로 만들어야 하는지는 설치 시 
:ref:`pip` 옵션을 이용하여 결정합니다. [1]_


Requirements files
------------------

:ref:`Requirements Files <pip:Requirements Files>`\은 단순합니다. 
:ref:`pip:pip install`\에 대한 인수를 파일에 목록으로 남긴 것입니다.

``install_requires``\는 하나의 프로젝트에 대한 의존성을 정의하는 반면, 
:ref:`Requirements Files <pip:Requirements Files>`\는 완전한 파이썬 환경을 위한
요구사항을 정의하는 데 사용됩니다.

``install_requires``\의 요구사항이 최소지만, 완벽한 환경을 
:ref:`repeatable installations <pip:Repeatability>`\에 아카이빙하여 자주 사용되는
고정된 버전을 철저히 관리하는데 사용됩니다.

``install_requires`` 요구 사항은 "추상적(Abstract)" 이기에 특정 인덱스와 관련이 없습니다.
요구사항 파일에는 "--index-url", "--find-links"와 같은 pip 옵션이 포함되어 요구사항을 
"고정(Concrete)" 하기에 패키지의 특정 인덱스나 디렉터리와 연관됩니다. [1]_

``install_requires`` 메타데이터는 설치 중에 pip에 의해 자동으로 분석되는 반면,
요구사항 파일은 사용자가 ``pip install -r`` 명령을 사용하여 설치할 때만 사용됩니다.

----

.. [1] For more on "Abstract" vs "Concrete" requirements, see
       https://caremad.io/2013/07/setup-vs-requirement/.
