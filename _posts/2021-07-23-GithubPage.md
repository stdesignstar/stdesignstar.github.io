---
title: 깃허브 페이지 로컬 구성
author: stdesignstar
date: 2021-07-23 17:00:00 +09:00
categories: [Github Page]
tags: [Github Page]
math: true
mermaid: true
---
<!--
- [1. git 설치](#1-git-설치)
- [2. 루비(RUBY) 설치](#2-루비ruby-설치)
- [3. 지킬(JEKYLL) 설치](#3-지킬jekyll-설치)
- [4. 예외처리](#4-예외처리)
- [5. 웹브라우저로 접속](#5-웹브라우저로-접속)
-->

깃허브 페이지 구성하면서, 로컬에서 미리 적용해보기 위해 다음과 같은 작업을 진행한다.  
os는 windows다.

## 1. git 설치

https://git-scm.com/

## 2. 루비(RUBY) 설치

https://rubyinstaller.org/downloads/archives/  

루비 인스톨러 홈페이지에서 Ruby+Devkit 2.4.4-1을 다운로드한다.  
(github에서 사용중인 루비버전이 2.4.4-1 이라 맞춰야 한다고 알고 있으나
해당 버전을 설치하면 아래과정이 진행이 안되서 본인은 최신버전을 설치했다.)

## 3. 지킬(JEKYLL) 설치

Start Command Prompt with Ruby를 실행한다.  
  
콘솔창에서 gem 명령어를 통해 지킬과 실행에 필요한 패키지들을 설치한다.  

```cs
gem install jekyll
gem install minima
gem install bundler
gem install jekyll-feed
gem install tzinfo-data
```

블로그 저장 폴더로 이동한다.  
```cs
cd e:/github/stdesignstar.github.io
```

지킬을 실행한다.
```cs
jekyll serve
```

## 4. 예외처리

[1] 인코딩관련
다음과 같은 에러가 발생한다면 인코딩 관련 이슈다.  
```cs
Invalid CP949 character "\xE2" on line 54
```

다음의 코드를 실행한뒤 지킬을 실행한다.
```cs
chcp 65001
```

[2] Dependencies 관련
dependencies 관련 오류가 발생할 경우 다음과 같이 지킬을 실행한다.
```cs
bundle exec jekyll serve
```

번들러는 Ruby에서 필요한 정확한 gem과 버전을 추적하고 설치하여 루비 프로젝트를 위한 일관된 환경을 제공한다.
번들러는 의존성 지옥에서 벗어나게 하고, 필요한 gem이 개발, 스테이징, 프로덕션에 있는지 확인해 준다.  

## 5. 웹브라우저로 접속
웹브라우저를 열고 http://127.0.0.1:4000/ 로 접속하면 본인의 블로그를 확인할 수 있다.