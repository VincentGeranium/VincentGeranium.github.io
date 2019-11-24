---
layout: post
title:  "What is the Segue(세그란?)? - Summary"
date:   2019-11-24
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 세그란?](https://www.edwith.org/boostcourse-ios/lecture/16893/)

- - -

### What is the Segue?

- `스토리보드`에서 뷰 컨트롤러 사이의 `화면전환`을 위해 사용하는 객체

- `별도의 코드 없이`도 스토리보드에서 `세그를 연결`하여 `뷰 컨트롤러 사이의 화면전환을 구현`할 수 있다

- - -

### UIStoryboardSegue Class

- UIStoryboardSegue Class는 UIKit에서 사용할 수 있는 표준 화면전환을 위한 프로퍼티와 메서드를 포함하고 있다

- 또 커스텀 전환을 정의하기 위해 서브클래스를 구현해서 사용할 수도 있다

- 필요에 따라서 UIViewController의 performSegue(withIdentifier:sender:) 메서드를 사용하여 세그 객체를 코드로 실행할 수 있다

- 세그 객체는 뷰 컨트롤러의 뷰 전환과 관련된 정보를 가지고 있다

- 세그는 뷰 컨트롤러의 뷰를 다른 뷰 컨트롤러의 뷰로 전환할 때 뷰 컨트롤러의 prepare(for:sender:) 메서드를 사용하여 새로 보여지는 뷰 컨트롤러에 데이터를 전달할 수 있다

- - -

### 주요 프로퍼티

- var source: UIViewController -> 세그에 전환을 요청하는 뷰 컨트롤러

- var destination: UIViewController -> 전환될 뷰 컨트롤러

- var identifier: String? -> 세그 객체의 식별자

- - -

### 주요 메서드

- func perform() -> 뷰 컨트롤러의 전환을 수행한다

- - -

### 인터페이스 빌더의 세그  연결

- 1) 스토리보드에서 전환될 뷰 컨트롤러를 객체 라이브러리로부터 드래그 앤 드롭으로 추가한다

![segueImg1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg1.png?raw=true)

- 2) 기존 뷰 컨트롤러의 뷰와 구분하기 위하여 새롭게 생성된 뷰 컨트롤러의 뷰를 선택하여 배경색을 변경한다

![segueImg2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg2.png?raw=true)

- 3) 첫 번째 뷰 컨트롤러의 뷰 위에 객체 라이브러리로부터 버튼을 추가하고 역활을 알려주기 위하여 "Show orange VC" 로 title을 변경한다

![segueImg3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg3.png?raw=true)

- 4) 버튼에서부터 키보드의 control키를 누른 상태로 드래그하여 전환될 뷰 컨트롤러에 드롭하여 연결한다

![segueImg4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg4.png?raw=true)

- 5) 세그의 종류 중 Show를 선택한다 `(Show 세그는 iOS 에서 현재 기기나 화면 상태에서 가장 적절한 화면전환 방식을 판단하여 화면을 전환해준다)`

![segueImg5](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg5.png?raw=true)

- 6) 두 뷰컨트롤러 사이에 세그가 생성된 것을 확인

![segueImg6](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg6.png?raw=true)

- 7) 시물레이터를 실행하여 버튼을 눌러 뷰가 전환되는 것을 확인

![segueImg7](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/segueImg7.gif?raw=true)
