---
layout: post
title:  "iOS 뷰 체계"
date:   2019-09-09
categories: iOS, Swift
---

# iOS View 체계

- iOS 애플리케이션 화면에서 보는 콘텐츠는 윈도우와 뷰를 사용해 나타난다.

- 원하는 모양으로 화면을 구성하고, 화면 위에서 일어나는 제스처를 관리하기 위해 뷰에 대해 이애하는 것은 중요.

---

## 뷰의 기본적인 역활

- iOS에서 화면에 애플리케이션의 콘텐츠를 나타내기 위해 윈도우와 뷰를 사용한다

- 윈도우는 ??

    - 그 자체로 콘텐츠를 표현할 수 없다

    - 그러나 애플리케이션의 뷰를 위한 컨테이너 역활을 한다.

- 뷰는 UIView 클래스 또는 UIView 클래스의 하위클래스(Subclass)의 인스턴스

    - 뷰는 윈도우의 한 영역에서 콘텐츠를 보여준다
    
- 뷰가 나타낼 수 있는 콘텐츠

    - 이미지, 문자, 도형등 다양하다
    
- 뷰는 또 다른 뷰를 관리하고 구성하기 위해 사용되기도 한다.

- 뷰는 제스처 인식기(gesture recognizer)를 사용하거나 직접 터치 이벤트를 처리할 수 있다.

- 뷰 계층(view hierarchy)구조에서 부모뷰(parent view)는 자식뷰(child view)의 위치와 크기를 관리한다.

- 나태나고자 하는 유형의 콘텐츠에 적합한 뷰를 여러 개 사용하여 뷰 계층(view hierarchy)구조를 구성하고 이를 통해 콘텐츠를 보여주는 것이 좋다

---

### View hierarchy (뷰 계층)

#### 뷰 계층 구조와 서브뷰 관리

- 뷰는 자신의 콘텐츠를 보여주는 것과 더불어, 다른 뷰를 위한 컨테이너로써의 역활도 한다.

    - 하나의 뷰가 다른 뷰를 포함할 때, 두 뷰 사이에 부모-자식 관계가 생성된다

        - 해당 관계에서 자식뷰는 서브뷰(subview), 부모뷰는 슈퍼뷰(superview)로 불려진다
        
        - 부모-자식 관계 형성은 애플리케이션의 시각적 모습과 동작 모두에 영향을 미친다.
        
- 슈퍼뷰는 하나의 배열 안에 서브뷰를 순서대로 저장한다
    
    - 만약 하나의 슈퍼뷰에 포함된 두 서브뷰가 서로 겹치게 되면, 나중에 추가된(또는 서브뷰 배열의 끝으로 옮겨진) 서브뷰가 맨 위에 보여지게 된다.
    
<img width="1500" height="1300" alt="image" scr="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/superviewAndsubview.png?raw=true">

---

#### 뷰 계층의 생성과 관리

- OS 애플리케이션에서 뷰 계층을 만드는 방법에는 인터페이스 빌더를 이용하는 방법과 코드를 작성하는 방법이 있다.

    - 코드작성 방식 사용시
    
        - 서브뷰를 부모뷰에 추가하기 위해, 부모뷰의 addSubView(_:) 메서드를 호출
        
            - 이 메서드는 해당 서브뷰를 서브뷰 목록의 마지막에 추가
            
        - 부모뷰의 서브뷰를 제거하기 위해서는 서브뷰의 removeFromSuperView() 메서드를 호출
        
        - 서브뷰를 부모뷰 목록의 중간에 삽입하기 위해 insertSubview(_:at:)
        
        - 부모뷰 내에 이미 존재하는 서브뷰를 정렬하기 위해 bringSubView(toFront:), sendSubview(toBack:)등의 메서드들을 호출할 수 있다.
        
---

### 뷰의 좌표계

- UIKit에서 기본이 되는 좌표계는 좌측 상단 모서리를 원점으로 한다

    - 원점으로부터 아래쪽, 오른쪽 방향으로 확장된다.
    
- 좌표값은 해상도와 상관없이 콘텐츠의 위치를 잡는 부동소수점을 사용하여 나타낸다

#### 프레임과 바운드

- iOS의 좌표체계의 시작은 왼쪽 위부터 시작

    - 즉, 제일 왼쪽의 제일 위의 지점이 (0,0)이다
    
    - 또, 수평축은 x로 수직축은 y로 표현한다.

- 뷰의 프레임(frame)은 뷰의 크기와 위치를 슈퍼뷰의 좌표계를 기준으로 나타낸다.

- 뷰의 바운드(bounds)는 뷰의 크기와 위치를 해당 뷰 자신의 좌표계를 기준으로 나타낸다.

<img width="1500" height="1300" alt="image" scr="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/originFrameBound.png?raw=true">

#### 프레임과 바운드 구현


<img width="1500" height="1300" alt="image" scr="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/originBoundsFrameExample.png?raw=true">

---

#### 뷰의 사각형을 정의하기 위해서 필요한 것들

- 1) 뷰는 어디에 그려져야 할지 위치를 알아야 한다

- 2) 위치로부터 어떤 크기로 그려져야 할지를 알아야한다

- 뷰의 프레임(frame)과 바운드(bounds)는 CGRect라는 구조체를 통해서 표현된다

- CGRect는 사각형의 크기와 위치에 대한 정보를 담고 있다.

- CGRect의 origin 프로퍼티는 CGPoint 타입으로 사각형의 시작점을 나타낸다

- CGRect의 size 프로퍼티는 CGSize 타입으로 사각형의 높이와 너비를 나타낸다

- CGPoint는 좌표를 표현할 수 있는 x와 y를 갖고 있다

- CGSize는 위치와 높이의 값인 width와 height를 갖고 있다.

- CGPoint의 x, y와 CGSize의 width, height는 모두 부동소수점 타입인 CGFloat으로 표현된다.


<img width="1500" height="1300" alt="image" scr="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/uiviewFrame.png?raw=true">


---

### 참고 문서 / 링크

- [Apple Documentation About Windows and Views](https://developer.apple.com/library/archive/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html)

- [Apple Documentation About View Programming Guide for iOS](https://developer.apple.com/library/archive/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW47)

- [edwith iOS의 View 체계](https://www.edwith.org/boostcourse-ios/lecture/16874/)

- [예제 실습 코드](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-09-09-view-hierarchy-example)








