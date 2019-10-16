---
layout: post
title:  "StackView Summary"
date:   2019-10-14
categories: iOS, Swift
---

이 포스트는 edwith의 boost coures iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍](https://www.edwith.org/boostcourse-ios/lecture/16884/)

- - -

### StackView

#### UIStackView

- 스택뷰는 여러 뷰들의 수평 또는 수직 방향의 선형적인 레이아웃의 인터페이스를 사용할 수 있도록 한다

- 스택뷰와 오토레이아웃 기능을 활용하여 디바이스 방향과 화면크기에 따라 동적으로 적응할 수 있는 사용자 인터페이스를 만들 수 있다

- 스택뷰의 레이아웃은 스택뷰의 "axis", "distribution", "alignment", "spacing"와 같은 프로퍼티를 통해 조정한다

- - -

- **수평(horizontal) axis 스택뷰 모식도**

![StackViewImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/stackViewImage.png?raw=true)

- - -

- **스택뷰는 "arrangedSubviews" 프로퍼티에 스택뷰에 포함된 뷰들을 관리한다**

    - 이 프로퍼티는 순서가 있는 배열과도 같다. 스택뷰에 포함된 뷰의 순서가 레이아웃에 영향을 미친다
    
![arrangedSubViewsImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/arrangedPropertyStackView.png?raw=true)


- - -

### 스택뷰의 생성

- 스토라보드에서 스택뷰에 뷰를 추가하는 것은 코드상에서 **func addArrangedSubview(UIView)** 메서드를 호출하는 것과 같다.

- - -

### 스택뷰를  먼저  생성하고  그 안에 새로운 뷰를 추가하는  방법

- 1) 스토리보드를 열고 객체라이브러리에서 스택뷰를 캔버스에 추가한다

![StackViewStoryboard-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-1.png?raw=true)

- 2) 객체라이브러리에서 버튼을 생성된 스택뷰에 추가

![StackViewStoryboard-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-2.png?raw=true)

![StackViewStoryboard-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-3.png?raw=true)

- 3) 또 하나의 버튼을 스택뷰에 추가한다. 버튼을 스택뷰에 포함된 버튼 옆으로 드래그하게 되면 커서 아래에 "Stack View"라는 텍스트가 나타나면서 드래그한 아이템을 스택뷰에 넣을 수 있게 도와준다

![StackViewStoryboard-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-4.png?raw=true)

- 스택뷰 안에 버튼 두 개가 추가된 것을 확인할 수 있다

![StackViewStoryboard-6](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-6.png?raw=true)

- 4) 버튼 두 개가 너무 붙어있다. 버튼 사이의 간격을 준다.

![StackViewStoryboard-5](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-5.png?raw=true)

- - -

### 이미 존재하는 뷰들을 스택뷰에 추가하는 방법

- 1) 스토리보드에서 객체라이브러리로부터 두 개의 버튼을 추가한다

![StackViewStoryboard-7](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-7.png?raw=true)

- 2) 두 개의 버튼을 선택 후 메뉴바에서 "Editor -> Embed In -> Stack View" 를 클릭하거나 캔버스 하단의 "Embed In Stack" 버튼을 클릭

![StackViewStoryboard-8](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-8.png?raw=true)

![StackViewStoryboard-9](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-9.png?raw=true)

- 3) 스택뷰 안에 버튼 두 개가 추가된 것을 확인

![StackViewStoryboard-10](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackViewStoryboard-10.png?raw=true)

- - -

### UIStackView 클래스의 주요 프로퍼티

- var  arrangedSubviews: [UIView]
    
    - 스택뷰의 정렬된 뷰의 배열이다. 스택뷰에 포함된 뷰들을 이 프로퍼티에 저장하고 관리한다
    
- var axis: UILayoutConstraintAxis

    - 레이아웃의 방향을 결정한다
    
    - **수직 : Verticla, 수평 : Horizontal**