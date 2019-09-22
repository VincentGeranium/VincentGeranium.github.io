---
layout: post
title:  "Navigation Interface란?"
date:   2019-09-22
categories: iOS, Swift
---

이 포스트는 부스트코스의 iOS 강의를 학습 후 정리한 내용입니다

- - -

### What is the Navigation Interface ?

- iOS 에서 내비게이션 인터페이스는 주로 계층적 구조의 화면전환을 위해 사용되는 드릴 다운 인터페이스(drill-down interface)이다.

    - 드릴 다운 인터페이스(drill-down interface)란 아래의 그림과 같이 각 선택할 수 있는 항목에 대한 세부항목이 존재하는 인터페이스이다.
    
![drilldownImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/navigationInterface.png?raw=true)

**내비게이션 인터페이스는 내비게이션 컨트롤러를 통해 구현한다**

- - -

### What is the Navigation Controller ?

- 내비게이션 컨트롤러는 컨테이네 뷰 컨트롤러(container view controller)로써 내비게이션 스택(navigation stack)을 사용하여 다른 뷰 컨트롤러(view controller)를 관리한다.

- 여기서 내비게이션 스택(navigation stack)에 담겨서 콘텐츠를 보여주게 되는 뷰 컨트롤러들을 컨텐트 뷰 컨트롤러(content view controller)라고 한다.

- 내비게이션 컨트롤러는 두 개의 뷰를 화면에 표시한다

    - 하나는 내비게이션 스택뷰(navigation stack view)에 포함된 최상위 컨텐트 뷰 컨트롤러(content view controller)의 콘텐츠를 나타내는 뷰(view)
    
    - 또 다른 하나는 내비게이션 컨트롤러(navigation controller)가 직접 관리하는 뷰(내비게이션 바 또는 툴바)
    
- 추가로 내비게이션 인터페이스의 변화에 따른 특정 액션을 동작하도록 하기 위해 내비게이션 델리게이트 객체를 사용할 수 있다

![navigationController](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/navigationController.png?raw=true)

- - -

### What is the Navigation Stack ?

- 내비게이션 컨트롤러에 의해 관리되는 내비게이션 스택(Navigation Stack)은 뷰 컨트롤러(View Controller)를 담을 수 있는 배열(Array)과도 같다

- 내비게이션 스택에 가장 하위에 있는(가장 먼저 스택에 추가된) 뷰 컨트롤러(View Controller)는 내비게이션 컨트롤러의 루트 뷰 컨트롤러(Root View Controller)가 된다.

- 루트 뷰 컨트롤러(Root View Controller)는 내비게이션 스택에서 팝(Pop)되지 않는다.

- 내비게이션 스택의 가장 상위에 있는(가장 마지막에 푸시(Push)된) 뷰 컨트롤러는 최상위 뷰 컨트롤러로 화면에 보이게 된다.

![navigationStackImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/navigationStack.png?raw=true)

- 이름에서 알 수 있듯이 내비게이션 스택은 push/pop를 통하여 Item(View Controller)을 관리한다.

- 새로운 뷰 컨트롤러를 내비게이션 스택에 push 하거나 내비게이션 스택에 있는 뷰 컨트롤러를 삭제하기 위해 pop를 사용한다.

- 내비게이션 스택에 push 된 각 view controller들은 애플리케이션에 자신이 가지고 있는 뷰 계층 구조를 통해  콘텐츠를 표시하게 된다.

- - -

### How do I Move View In Navigation Stack ?

- UINavigationController 클래스의 메서드 또는 segue를 사용하여 내비게이션 스택의 뷰 컨트롤러를 추가/삭제할 수 있다

*세그(Sugue) : 세그는 스토리보드에서 한 화면에서 다른 화면으로 전환을 말한다. 세그도 내부적으로 UINavigationControlller 클래스의 메서드를 사용한다*

- 애플리케이션 실행 중 사용자가 내비게이션 인터페이스의 뒤로가기(back) 버튼을 사용하거나 화면의 왼쪽 가장자리를 스와이프(Swipe)하여 스택에 있는 최상위 뷰 컨트롤러를 삭제하고 그 아래에 가려져 있던 뷰 컨트롤러의 콘텐츠를 보여줄 수도 있다.

- - -

### Push of Navigation Stack

**내비게이션 스택에 새로운 뷰 컨트롤러가 푸시(push) 될 때 UIViewContoroller 인스턴스가 생성되고 내비게이션 스택에 추가된다.**

- 1) 가장 먼저 내비게이션 스택에 루트 뷰 컨트롤러만 들어가 있는 초기상태.

    - **내비게이션 컨트롤러를 생성할 때 반드시 루트 뷰 컨트롤러가 설정되어 있어야 한다**

![naviPushImage_1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/naviPushImage_1.png?raw=true)

- 2) `뷰 컨트롤러 1로 이동` 이라는 버튼을 통해서 내비게이션 스택에 뷰 컨트롤러 1을 푸시(push)한다. 

    - 뷰 컨트롤러1의 인스턴스가 생성되고 내비게이션 스택에 추가된다. 

    - 뷰 컨트롤러1이 최상위 뷰 컨트롤러로써 화면에 보이게 된다.

![naviPushImage_2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/naviPushImage_2.png?raw=true)

- 3) `뷰 컨트롤러2로 이동`이라는 버튼을 통해서 내비게이션 스택에 뷰 컨트롤러2도 푸시한다.

    - 뷰 컨트롤러2의 인스턴스가 생성된다, 내비게이션 스택에 추가된다.
    
    - 뷰 컨트롤러 2가 최상위 뷰 컨트롤러로써 화면에 보이게 된다.
    
**여기서 주목할 점은 새로운 뷰 컨트롤러가 추가될 때도 아래에 있는 뷰 컨트롤러들(인스턴스)이 삭제되지 않고 유지되고 있다는 점이다.**

![naviPushImage_3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/naviPushImage_3.png)



