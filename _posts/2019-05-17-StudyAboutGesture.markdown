---
layout: post
title:  "Gesture Recognizer 와 touchesBegan - 190517"
date:   2019-05-17
categories: iOS, Swift
---

# What is Gesture ??

---

#### 출처

이 포스트는 ZeddiOS 님의 블로그를 참고하여 쓴 포스트임을 미리 밝힙니다

[ZeddiOS님의 블로그](https://zeddios.tistory.com/112)

---

# Gesture ?

- 화면을 터치를 하거나, 사진을 넘겨보기 위해 옆으로 스와이프 하는 행동이나 지도의 확대를 위해 손가락으로 넓히는 행동들을 제스쳐라고 한다

---

# 제스쳐를 구현하는 방법 ?

#### 제스쳐를 구현하는 방법에는 2가지가 있다

1. touchesBegan/Ended/Moved/Cancelled -> method

2. Tap Gesture Recognizer 를 포함한 다양한 제스쳐 -> StoryBoard

---

# Gesture Recognizer

모든것을 설명하기에는 너무 길기 때문에 TapGestureRecognizer를 예를 들어 설명

- Tap Gesture Recognizer도 button, label과 마찬가지로 @IBAction과 @IBOutlet 이 존재함

--- 

# Gesture Recognizer 와 touchesBegan 등 비교 구현 링크

- GestureRecognizer method를 이용하여 각 method의 호출시점 확인 [github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-05-17-TapGestureRecognizer)

- Tap gesture recognizer 와 touchesBegan 간의 호출 시점과 호출 시점 비교 [github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-05-17-GestureRecoginze-StoryBoard)
