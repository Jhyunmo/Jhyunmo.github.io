---
title:  "UGUI MultiTouch Control" 
date: 2023-06-04
categories:
  - UnityStudy
tags:
  - [UnityStudy]

toc: true
toc_sticky: true

last_modified_at: 2023-06-04
---

# MultiTouch
>유니티에서 UGUI MultiTouch를 지원하지 않으려면 게임 시작 초기화 부분에서 간략하게 제어할 수 있다.

  ```c#
Input.multiTouchEnabled = false;
  ``` 
## 만약 특정 UI에서만 MultiTouch를 제어하고 싶다면 해당 부분 Event에서 아래 구문을 사용하면 된다.
  ```c#
if(input.touchCount > 1) return;
  ``` 