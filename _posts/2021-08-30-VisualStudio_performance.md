---
title: Visual Studio 성능 향상
author: stdesignstar
date: 2021-08-30 12:00:00 +09:00
categories: [Visual Studio]
tags: [Visual Studio,Unity]
math: true
mermaid: true
---

## 개요

유니티 IDE로 VisualStudio를 사용하고 있다.  
어느 순간 VisualStudio가 너무 느려 타자치는 속도가 버벅이는 정도가 되더라.  
성능 향상을 위해 사용하지 않는 기능을 해제한다.  

## 본문  

도구 - 옵션 - 환경 - 일반 -  
"클라이언트 성능을 기준으로 시각적 환경을 자동으로 조정",  
"리치 클라이언트 시각적 효과 사용"  
"사용 가능한 경우 하드웨어 그래픽 가속 사용"  
체크 해제

도구 - 옵션 - 환경 - 계정  
"Visual Studio에 로그인할때 장치의 설정을 동기화"  
체크 해제

도구 - 옵션 - 환경 - 시작  
"콘텐츠 다운로드 간격"  
체크 해제

도구 - 옵션 - 환경 - 탭 및 창  
"미리 보기 탭"
 체크 해제  

도구 - 옵션 - 환경 - 확장 및 업데이트  
모두 체크 해제

도구 - 옵션 - 소스 제어  
"현재 소스 제어 플러그 인"  
None으로 전환  

도구 - 옵션 - 텍스트 편집기 - C# - Intellisense  
"완성 항목 필터 표시"  
체크 해제  

도구 - 옵션 - Tool for Unity - 탐색기  
"솔루션 탐색기 동기화" 
False

도움말 - 피드백 보내기 - 설정  
환경 개선 프로그램에 참여하지 않습니다.  

도구 - 옵션 - 프로젝트 및 솔루션  
"솔루션 로드 시 문서 다시 열기"  
체크 해제  

Solution Explorer 보다 Unity Project Explorer 를 사용한다.  
View > Unity Project Explorer  

## Reference  
https://unity.com/kr/how-to/tips-optimize-your-visual-studio-tools-when-coding-unity