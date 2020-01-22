---
layout: post
title:  "Tab Bar Summary"
date:   2020-01-15
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - About TabBar](https://www.edwith.org/boostcourse-ios/lecture/16862/)

- - -

### About TapBar

- `화면 하단에 위치하며 뷰 컨트롤러 사이의 화면전환을 위해 사용되는 인터페이스.`

- 사용자가 `탭바의 항목(Item)을 선택`하면 해당` 항목에 연결된 뷰 컨트롤러의 콘텐츠`가 `화면`에 보이게 된다.

- `주로 여러 메뉴를 구성할 때 많이 사용한다.`

- `카테고리 사이의 전환`을 위해 사용하거나 `다양한 관점으로 같은 정보를 제공`하는 데 사용한다.

- 탭바는 화면에 보여지기 위한 뷰 요소이므로 `제어를 하기 위해서는 컨트롤러가 필요하다.`

- 프로그래머가 직접 탭바를 제어할 컨트롤러 클래스를 작성하여 사용할 수도 있지만, `대부분의 경우 프레임워크에서 제공하는 탭바 컨트롤러(UITabBarController)를 사용하여 제어한다.`

- `탭바와 탭바 컨트롤러를 사용하여 인터페이스를 구성한 것을 탭바 인터페이스라고 부른다.`

![TabBarImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-1.png?raw=true)

- - -

### 탭바의 구조

- `탭바 인터페이스`는 탭바 컨트롤러가 생성한 `탭바 뷰(View)`와 탭바 컨트롤러가 관리하는 `콘텐츠 뷰 컨트롤러`로 `구성`되어 있다.

- `탭바 컨트롤러`는 연결된 콘텐츠 뷰 컨트롤러의 `컨테이너 뷰 컨트롤러`이다.

- `각 콘텐츠 뷰 컨트롤러`는 탭바에서 `하나의 탭`에 해당한다.

- 사용자가 `탭바에서 탭을 선택`할 때, `탭바 컨트롤러 객체`가 `해당 콘텐츠 뷰 컨트롤러의 뷰`를 `화면`에 보여준다.

![TabBarImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-2.png?raw=true)

- - -

### 탭바 인터페이스 생성하기

#### 객체라이브러리 사용 방법

![TabBarImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-3.png?raw=true)

- 1) 탭바 컨트롤러를 객체 라이브러리로부터 드래그한다.

![TabBarImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-4.png?raw=true)

- 2) 생성된 탭바 컨트롤러를 선택한 후 속성 인스펙터 탭에서 Is Initial View Controller 옵션을 선택한다.

    - Is Initial View Controller 옵션을 스토리보드의 컨트롤러 중에 하나만 설정할 수 있으며, 해당 스토리보드의 맨 처음 진입화면이 된다.
    
- - -

### 이미 존재하는 뷰 컨트롤러를 탭바 컨트롤러에 연결하기

#### 기존에 존재하는 뷰 컨트롤러를 탭바 컨트롤러에 연결

![TabBarImage-5](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-5.png?raw=true)

- 1) 기존에 있는 뷰 컨트롤러(들)을 선택하고 Editor -> Embed in -> Tab bar controller를 선택하여 뷰 컨트롤러를 탭바 컨트롤러에 포함시킨다.

- - -

### 탭바 컨트롤러에 뷰 컨트롤러 추가하기

![TabBarImage-6](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-6.png?raw=true)

- 1) 탭바 컨트롤러에 새롭게 추가할 뷰 컨트롤러를 생성한다.

![TabBarImage-7](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-7.png?raw=true)

- 2) 탭바 컨트롤러에서부터 키보드의 'control'키를 누른 상태로 드래그하여 추가할 뷰 컨트롤러에 드롭하여 세그(Segue)창이 나타나면 Relation Segue의 view controllers를 선택한다

![TabBarImage-8](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TabBarImage-8.png?raw=true)

- 3) 탭바 컨트롤러에 뷰 컨트롤러가 새롭게 추가된 것을 확인할 수 있다.

- - -

### About TapBar Item

- 탭바 뷰에서 각 탭은 이름과 이미지를 표시할 수 있고 뷰 컨트롤러는 이러한 용도로 tabBar프로퍼티를 관리한다.

- 탭바 컨트롤러가 콘텐츠 뷰 컨트롤러를 포함하면 해당 뷰 컨트롤러의 탭바 아이템이 탭바 컨트롤러의 탭바에 추가된다.

- 탭바 컨트롤러의 탭바 아이템이 6개 이상인 경우, 5번째 탭에 'More'이라는 아이템이 표시되고 사용자가 'More' 버튼을 누르면 나머지 탭 항목을 선택 할 수 있는 인터페이스가 표시된다.

- - -

### UITabBarControllerDelegate

- 사용자가 탭바 인터페이스와 상호작용할 때, 탭바 컨트롤러 객체는 이 상호작용에 관한 알림(notification)을 델리게이트 인스턴스로 보낸다.

- 사용자가 탭을 선택하지 못하게 하거나, 탭을 선택한 후 추가 작업을 수행하거나, 탭 관련 사항을 모니터링하고 사용자화 하기 위해서 델리게이트를 활용한다

[Apple Developer Documentation - UITabBarControllerDelegate](https://developer.apple.com/documentation/uikit/uitabbarcontrollerdelegate)

- - -

### UITabBarController Class

- UITabBarController Class에는 탭바를 구성하고 각 탭에 해당하는 뷰 컨트롤러들을 관리하기 위한 메서드와 프로퍼티가 정의되어 있다

    - 탭바 컨트롤러의 탭을 구성하기 위해서는 뷰 컨트롤러를 탭바 컨트롤러의 viewControllers 프로퍼티에 할당한다.
    
    - 탭바 아이템은 해당 탭에 연결된 뷰 컨트롤러를 통해 구성한다. 
    
    - UITabBarItem 클래스의 인스턴스를 뷰 컨트롤러의 tabBarItem 프로퍼티에 할당한다.
    
    - 만약 UITabBarItem 클래스의 인스턴스를 뷰 컨트롤러에 따로 할당하지 않을 경우, 탭바에는 이미지 없이 뷰 컨트롤러의 title 프로퍼티에 해당하는 텍스트로만 탭바의 항목으로 표시된다.
    
- - -

### About View of TabBar Controller

- UITabBarController 클래스는 UIViewController 클래스를 상속받기 때문에 TapBarController는 view 프로퍼티를 통해 접근할 수 있는 자신만의 자체 뷰(view)를 가지고 있다.

    - 이 뷰는 탭바와 선택된 뷰 컨트롤러의 콘텐츠를 나타내는 뷰로 구성되어 있다.
    
- - -

### UITabBarController 클래스의 주요 프로퍼티 및 메서드

- var tabBar: UITabBar

    - 탭바 컨트롤러와 연결된 탭바 뷰
    
- var viewControllers: [UIViewController]?

    - 탭바 컨트롤러가 관리하는 뷰 컨트롤러의 배열
    
    - 즉, 각각의 탭바 항목에 해당하는 뷰 컨트롤러의 목록
    
- func setViewControllers([UIViewController], animated: Bool)?

    - 탭바 컨트롤러가 관리할 뷰 컨트롤러들을 설정
    
- var selectedViewController: UIViewController?

    - 현재 선택된 탭 항목과 연결된 뷰 컨트롤러
    
- var selectedIndex: Int

    - 현재 선택된 탭 항목의 인덱스(index)