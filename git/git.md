# git 사용법

## git 정의

> 분산 버전 관리 시스템

diff가 어떤 부분인지 알고 수정 사항을 남긴다.

## git bash

> CLI 형태, 오류 발생시 오류를 보는 명령어 필요

## git 명령어

- git 파일 및 저장소 생성

  ```bash
  $ git init
  ```

- staging area 으로 변경 사항 이동

  ```bash
  $ git add [파일, 폴더 이름 or . or -a]
  ```

- staged  된 파일이나 폴더를 버전 기록

  ```bash
  $ git commit -m "메시지"
  ```

- git push - commits 새로 반영

  ```bash
  $ git push origin main 
  ```

- git commit log 확인

  ```bash
  $ git log 
  $ git log --oneline 
  $ git log -2 
  ```

  [git log 옵션 내용](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%BB%A4%EB%B0%8B-%ED%9E%88%EC%8A%A4%ED%86%A0%EB%A6%AC-%EC%A1%B0%ED%9A%8C%ED%95%98%EA%B8%B0)

- git 설정

  ```bash
  $ git config --list
  ```

- 현재 상태 위치와 이전 상태 위치 비교 

  ```bash
  $ git diff HEAD HEAD~1
  $ git diff HEAD HEAD~2
  ```

  



