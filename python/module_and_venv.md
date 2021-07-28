# 모듈과 가상환경

## 모듈

- 특정 기능을 파이썬 파일로 작성한 것

- 패키지
  - 모듈 집합
  - 패키지 내부 서브 패키지 존재

- 파이썬 표준 라이브러리 Python Standard Library PSL
  - 기본적으로 내장된 모듈과 함수

- 파이썬 패키지 관리자 pip

  - PyPI 외부 패키지들을 설치하도록 돕는 패키지 관리 시스템

  - [사이트](https://pypi.org/)

  - 사용법

    ```bash
    $ pip install [package name]
    $ pip install [package name==version]
    $ pip uninstall [package name]
    $ pip list
    $ pip show [package name]
    $ pip freeze > requirements.txt # 패키지 관리
    $ pip install -r requirements.txt # 패키지 목록 설치
    ```

## 가상환경

- 프로젝트 별로 버전이 다른 경우 가상환경을 사용해 독립적으로 패키지를 관리한다.

- venv

  - 가상 환경을 만들고 관리하는 모듈

  ```bash
  $ python -m venv [폴더명 default venv]
  $ /venv/Scripts/activate # 활성화
  $ deactivate # 비활성화
  ```

## 패키지

- 여러 모듈과 하위 패키지로 구성

- 폴더 내부에` __init__.py` 파일ㄹ로 패키지로 인식, python 3.3 버전 이상부터 필요 없지만 하위 버전 호환을 위해 사용

  

