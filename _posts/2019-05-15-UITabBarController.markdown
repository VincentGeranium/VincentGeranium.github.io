---
layout: post
title:  "UITabBarController에 대한 간략한 설명 - 190515"
date:   2019-05-15
categories: iOS, Swift
---

# UITabBarController

---

#### 출처

- 이 포스트는 꿈꾸는 개발자님의 "UITabBarController" 포스트를 참조하여 쓴 포스트 임을 미리 밝힙니다

[꿈꾸는 개발자님의 블로그](https://m.blog.naver.com/PostView.nhn?blogId=scw0531&logNo=220852115735&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

---

# Tap UI 구성 방법

- **탭은 하나의 화면안에 여러개의 화면이 중첩된 형태로 구성되는 UI**

- 탭은 UI를 구성 시 불필요한 화면 절약 가능

- 사용자가 화면의 이동없이 한 화면에서 여러가지 정보를 동시에 획득 가능

- 많은 정보를 보여주기 위해 한정된 스마트폰의 화면에서 탭의 사용은 굉장히 유용하다

---

# iOS에서의 Tab의 구성

- **큰 구조로 탭의 전체적인 구조를 담당하는 UITabBar**

- **UITabBar 내부에 UITabBarItem이 존재**

- 탭에서 아이템의 역활은 현재 사용자가 보고있는 화면의 indicator 정보를 알려준다

- 아이템은 **선택된 경우와 선택되지 않은 경우** 두가지로 나뉜다

- 아이템을 두 가지로 구분해주는 이유는 **사용자에게 보여질 때 선택된것에 대한 구분이 없으면 현재 어떤 탭 화면에 위치하고 있는지 알 수가 없다** 따라서 항상 두 가지의 이미지를 같이 고려해야 한다

- 아이템에 대한 이름을 넣을 수 있다. 이름(Title)이 들어가면 사용자에게 좀 더 명확히 탭의 정보를 알려줄 수 있다.

---
