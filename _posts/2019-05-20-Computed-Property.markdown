---
layout: post
title:  "Computed Property - 190520"
date:   2019-05-20
categories: iOS, Swift
---

# Computed Property

---

#### 출처

이 포스트는 ZeddiOS님의 Swift ) Properties - Computed Property(연산 프로퍼티)의 글을 참고하였음을 미리 밝힙니다

[ZeddiOS님의 Swift ) Properties - Computed Property(연산 프로퍼티)의 글](https://zeddios.tistory.com/245)

---

- **연산 프로퍼티는**값을 "저장"하기 보다는 그때그때 특정한 연산을 통해 값을 리턴

- 클래스, 구조체, 열거형에서 사용

- **getter, setter를 통해 다른 프로퍼티와 간접적으로 값을 검색하고 세팅**

- **getter과 setter를 사용하려면 그 연산된 값을 저장할 변수가 반드시 있어야 한다**

- 연산 프로퍼티는 반드시 **var**로 선언

- get만 있는 연산 프로퍼티는 Read-Only Computed Properties **읽기 전용 연산 프로퍼티**라고 한다

- get,set을 동시에 구현이 가능

- get 만 구현 가능

- set 만 구현 불가능

- set의 파라미터를 생략할 수 있으며 생략했을 시, newValue라는 키워드를 사용한다
