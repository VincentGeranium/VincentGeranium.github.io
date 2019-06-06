---
layout: post
title:  "AutoLayout 에 대한 간략한 정리"
date:   2019-06-06
categories: Swift, iOS
---

### 참고 자료

이 포스트는 edwith의 iOS 부스트코스 강좌를 듣고 정리된 내용을 참고로 하여 쓴 포스트임을 미리 밝힙니다.

[edwith iOS 부스트코스](https://www.edwith.org/boostcourse-ios/lecture/16848/)

---

# What is AutoLayout

- AutoLayout은 뷰의 제약 사항을 바탕으로 뷰 체계 내의 모든 뷰의 크기와 위치를 동적으로 계산

- AutoLayout은 Application을 사용할 때 발생하는 외부 변경과 내부 변경에 동적으로 반응하는 사용자 인터페이스를 가능하게 한다

---

# About External Changes (외부 변경)

외부 변경은 슈퍼뷰의 크기나 모양이 변경될 때 발생.

**각각의 변화와 함께, 사용 가능한 공간을 잘 사용할 수 있도록 뷰 체계의 레이아웃을 업데이트 해주어야 한다**

---

## 외부 변경이 발생하는 경우

- 사용자가 아이패드의 분할뷰(Split View)를 사용하거나 사용하지 않는 경우(iOS)

- 디바이스를 회전하는 경우(iOS)

- 활성화콜(Active Call)과 오디오 녹음 바가 보여지거나 사라지는 경우(iOS)

- 다른 크기의 클래스를 지원하기 원하는 경우

- 다른 크기의 스크린을 지원하기 원하는 경우

---

### 외부 변경이 발생하는 경우에 대한 설명

외부 변경이 발생하는 경우, 대부분 실행 시간에 발생할 수 있으며, 애플리케이션으로부터 동적인 응답을 요구한다.

다른 스크린 크기를 지원하는 것과 같은 것은 애플리케이션이 다른 환경에 적응하는 것을 나타낸다.

스크린 크기가 일반적으로 실행 시간에 변경되지 않는다고 하더라고, **적응형 인터페이스**를 만들면 애플리케이션이 

아이폰 4S, 아이폰 6플러스, 또는 아이패드에서도 모두 동일하게 잘 작동할 수 있다

**오토레이아웃은 아이패드 내부 변경에서 슬라이드와 분할뷰를 지원하는 핵심 요소이기도 하다**

---

# About Internal Changes (내부 변경)

**내부 변경은 사용자 인터페이스의 뷰의 크기 또는 설정이 변경되었을 때 발생**

---

## 내부 변경이 발생하는 경우

- 애플리케이션 변경에 의해 콘텐츠가 보여지는 경우

- 애플리케이션이 국제화를 지원하는 경우

- 애플리케이션이 동적 타입을 지원하는 경우

---

### 내부 변경이 발생하는 경우에 대한 설명

**애플리케이션 콘텐츠가 변경됐을 때, 새로운 콘텐츠는 예전과 다른 레이아웃을 필요 할 수 있다**

예를 들어 신문기사를 제공하는 애플리케이션이 각각의 신문 기사의 크기에 기반을 둔 레이아웃을 조정할 필요가 있는 경우과 같이,

텍스트 또는 이미지를 보여주는 애플리케이션에서 일반적으로 발생하는 일이다

이와 비슷하게, 사진 콜라주는 이미지 크기와 영상의 가로 세로의 비율을 다뤄야만 한다

---

# 오토레이아웃의 필요성

**오토레이아웃은 인터페이스의 절대적인 좌표가 아닌 동적으로 상대적인 좌표가 필요한 경우에 유용**

- 애플리케이션이 실행되는 iOS 기기의 스크린 화면의 크리가 다양한 경우

- 애플리케이션이 실행되는 iOS 기기의 스크린이 회전할 수 있는 경우

- 상태표시줄(Status Bar)에 전화 중임을 나타내는 액티브 콜(active call)과 오디오 녹음 중임을 나타내는 오디오 바가 보여지거나 사라지는 경우.

- 애플리케이션의 콘텐츠가 동적으로 보여지는 경우

- 애플리케이션이 지역화(Localization)를 지원하는 경우

- 애플리케이션이 동적 타입을 지원하는 경우

---

# 오토레이아웃 속성

**오토레이아웃의 속성은 정렬 사각형을 기반으로 한다**

![AutoLayoutImage](https://user-images.githubusercontent.com/42841888/59020182-6e5a8f00-8884-11e9-8935-a17b7cccad1a.png)

- Width : 정렬 사각형의 너비

- Height : 정렬 사각형의 높이

- Top : 정렬 사각형의 상단

- Bottom : 정렬 사각형의 하단

- Baseline : 텍스트의 하단

- Horizontal : 수평

- Vertical : 수직

- Leading : 리딩, 텍스트를 읽을 때 시작 방향

- Trailing : 트레일링, 텍스트를 읽을 때 끝 방향

- CenterX : 수평 중심

- CenterY : 수직 중심

--- 

# What is The Safe Area

안전 영역은 콘텐츠가 상태바, 네비게이션바, 툴바, 탭바를 가리는 것을 방지하는 영역

표준 시스템이 제공하는 뷰들은 자동으로 안전 영역 레이아웃 가이드를 준수해야 한다

기존의 상/하단 레이아웃 가이드(Top/Bottom Layout Guide)를 대체, 하위 버전에도 호환하여 작동

안전 영역은 iOS 11 부터 사용, iOS 11 미만의 버전에서는 상/하단 레이아웃 가이드를 사용

**안전 영역 레이아웃 가이드는 UIView 클래스의 var safeAreaLayoutGuide: UILayoutGuide로 접근할 수 있다**

![safeAreaImage](https://user-images.githubusercontent.com/42841888/59020663-6c450000-8885-11e9-883c-9a7e5add3e34.png)

---

# What is The Constraints

**constraints(제약)은 뷰 스스로 또는 뷰 사이의 관계를 속성을 통하여 정의**

제약은 방정식으로 나타낼 수 있다

![constraintsImage](https://user-images.githubusercontent.com/42841888/59032597-aa501d00-88a1-11e9-8571-2b29a24d167e.png)

- Item1 : 방정식에 있는 첫 번째 아이템(B View), **첫 번째 아이템은 반드시 뷰 또는 레이아웃 가이드이어야 한다**

- Attribute1 : 첫번째 아이템에 대한 속성, 이 경우 B View의 leading

- Multiplier : 속성 2에 곱해지는 값, 이 경우 1.0

- Item2 : 방정식에 있는 두 번째 아이템(A View)

- Attribute2 : 두번째 아이템에 대한 속성, 이 경우 A View의 trailing

- Constant : 두 번째 아이템의 속성에 더해지는 상수 값

**위 그림의 방정식의 제약을 해석하면 B View의 leading은 A View의 trailing의 1.0배에 8.0을 더한 위치**

---

# What is The Intrinsic Content Size(고유 콘텐츠 크기)

**뷰의 고유 콘텐츠 크기는 뷰가 갖는 원래의 크기로 생각할 수 있다. 예를 들어 레이블의 고유 콘텐츠 크기는 레이블의 텍스트 크기고, 이미지의 고유 콘텐츠 크기는 이미지 자체의 크기이다.**


---

# What is The Constraint Priorities(제약 우선도)

**오토레이아웃은 뷰의 고유 콘텐츠 크기를 각 크기에 대한 한 쌍의 제약을 사용하여 나타낸다.**

**우선도가 높을수록 다른 제약보다 우선적으로 레이아웃에 적용되며, 같은 속성의 다른 제약과 경합하는 경우, 우선도가 낮은 제약은 무시된다**

---

# 콘텐츠 허깅 우선도(Content hugging priority)

**콘텐츠 고유 사이즈보다 뷰가 커지지 않도록 제한한다.**

다른 제약사항보다 우선도가 높으며 뷰가 콘텐츠 사이즈보다 커지지 않는다

---

# 콘텐츠 축소 방지 우선도(Content compression resistance priority)

**콘텐츠 고유 사이즈보다 뷰가 작아지지 않도록 제한한다.**

다른 제약사항보다 우선도가 높으며 뷰가 콘텐츠 사이즈보다 작아지지 않는다

---

# Image of Content hugging priority and compression

![ContentImgae](https://user-images.githubusercontent.com/42841888/59033733-53981280-88a4-11e9-91e7-cbef8a227b0b.png)

---

# Layout Margins

**뷰에 콘텐츠 내용을 레이아웃 할 때 사용하는 기본 간격(default spacing)**

- Layout Margins Guide : 레이아웃 마진에 따라 형성되는 시각의 프레임 영역

---

# Anchor

**오토레이아웃을 코딩으로 구현하여 Constraint(제약)을 만들기 위해 Anchor을 사용할 수 있다**

---

# Layout Anchor 사용 예제

- 내 식으로 만들어본 예제 프로젝트 파일, [github](https://github.com/VincentGeranium/Swift-Study/tree/master/AutoLayout-Anchor-Example)

- edwith에 나온 예제 따라한 프로젝트 파일,  [github](https://github.com/VincentGeranium/Swift-Study/tree/master/Autolayout-Anchor-edwith-Example)

---
