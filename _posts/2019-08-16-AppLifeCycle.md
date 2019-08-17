---
layout: post
title:  "앱 생명주기"
date:   2019-08-16
categories: Swift, iOS
---

# App Life cycle

## The App Life Cycle

    앱은 개발자가 작성한 코드와 시스템 프레임워크간의 상호작용의 결과물
    
    프레임워크에서는 앱 실행 환경에 필요한 도구를 제공 또한 개발자가 원하는 느낌의 앱을 만들 수 있는 도구를 제공
    
    이러한 프레임워크를 효과적으로 사용하기 위해서 "iOS Infra structure"에 대한 이해가 필요하다
    
#### 요약

- 앱 = 개발자가 작성한 코드 and 시스템 프레임워크 간의 상호작용의 결과물

- 프레임워크 = 앱 실행 환경에 필요한 도구 제공, 개발자가 원하는 느낌의 앱을 만들 수 있는 도구 제공

- 프레임워크를 효과적으로 사용위해 **iOS Infra structure** 이해 필요
    
## iOS Framework

    iOS Framework는 MVC와 Delegation이라는 디자인패턴에 의존하고 있다
    
    완성도있는 앱을 제작하는데에 있어서 디자인 패턴을 이해하는것은 매우 중요하다

#### 요약

- iOS 프레임워크 = MVC 와 Delegation 디자인패턴에 의존
    - 즉, 앱을 제작하는데 디자인 패턴을 이해하는것은 매우 중요
    
## The Main Function
    
    모든 C언어 기반의 프로그램의 시작점은 main 함수이다.
    
    iOS 앱에서는 직접 main 함수를 작성하지 않는다.
    
    대신 Xcode에서 프로젝트에 main 함수를 생성해 준다.
    
    UIApplicationMain 함수는 앱에 몇가지 중요한 객체를 생성하고, 스토리보드에서 UI를 로딩하고,
    
    앱의 초기 셋팅값(info.plist)을 불러오고, 앱을 Run loop에 올려 놓으며 함수를 진행시킨다.
    
    개발자가 넘겨주는 값은 스토리보드 파일과 앱 초기 셋팅 정보 뿐이다.
    
#### 요약

- UIApplicationMain 함수 진행 조건
    - 앱에 몇가지 중요한 객체 생성
    - 스토리보드에서 UI 로딩
    - 앱의 초기 셋팅값(info.plist) 불러오기
    - 앱을 Run loop에 올려 놓음

- 개발자는 스토리보드 파일과 앱 초기 셋팅 정보만 넘겨줌
    
## The Structure of an App

    앱이 시작되면서 UIApplicationMain 함수는 몇가지 중요한 객체를 생성하고 앱을 실행시킨다
    
    모든 iOS 앱의 중심에는 시스템과 앱의 여러 객체들간의 대화를 가능하게 해주는 UIApplication 객체가 있다
    
## MVC 디자인패턴
    
<img width="670" alt="appStructure" src="https://user-images.githubusercontent.com/42841888/63178472-13fc5c80-c085-11e9-87b8-f657d2a42718.png">

    Model-View-Controller 구조
    
    이 디자인패턴은 앱의 Data와 비지니스 로직을 UI 요소로부터 분리를 시켜준다
    
## 중요 객체와 설명
    
#### 1. UIApplication

    Event loop 관리, 델리게이트(내가 정의한 커스텀 객체)에 앱 상태 변화나 푸쉬알림 같은 주요한 이벤트들을 알려줌
    
#### 2. App Delegate
    
    내가 작성한 코드의 핵심은 delegate이다
    
    이 객체는 UIApplication 객체와 함께 앱 초기화, 앱 상태 변화, 많은 high-level 이벤트 등을 관리한다
    
    이 객체는 앱에 하나만 존재 할 수 있도록 보장된다 때문에, 앱의 초기 자료구조를 설정하는데 주로 사용됨

#### 3. Documents and Data model

    Data model object는 앱의 콘텐츠를 저장하는데 사용되고 각 앱에 대한 고유성을 가진다
    
    예를들어, 그림을 그리는 앱은 이미지 객체를 저장하거나 그 이미지를 생성하기 위한 명령 Sequence를 저장 할 수 있다
    
    앱에서는 앱의 Data model object의 데이터 일부를 관리하기 위해 document object(UIDocument의 서브클래스)를 사용할 수 잇다
    
    Document 객체는 필수는 아니지만 파일에 저장된 그룹 데이터를 다루는데에 편리한 기능을 제공한다
    
#### 4. View Controller 객체
    
    View Controller 객체는 앱의 내용을 화면에 나타내는 기능을 함
    
    하나의 View Controller는 하나의 view와 이 뷰의 subview들을 관리한다
    
    화면에 view 가 표시될 때 view controller 객체는 뷰들의 앱의 window에 설치함으로써 보여지게 해준다
    
    UIViewController 클래스는 모든 view controller 객체의 부모클래스 이다
    
    이 클래스는 뷰를 로드하고, 나타내고, 디바이스의 회전에 따라 돌려주고, 여러 기본 동작에 대한 기능을 제공하고 있다
    
    UIkit과 또 다른 프레임워크에서 추가적으로 다른 view controller를 제공하고 있다
    
    Image picker, tab bar interface, navigation interface와도 같은 것들
    
#### 5. UIWindow 객체

    UIWindow 객체는 화면에 나타날 뷰들을 다룬다
    
    대부분의 앱들은 Main screen에 해당하는 Window 딱 하나만 가진다
    
    외부 디스플레이를 지원하기 위한 추가적인 window를 가질수도 있다
    
    앱 컨텐츠를 변경하려면 view controller를 사용하여 변경 -> 절대로 window를 변경하면 안된다
    
    뷰를 보여주는 역활 외에도, window는 UIApplication 객체와 같이 작동하여 viwe controller와 view에게 이벤트를 전달하는 역활을 한다
    
#### 6. view, control, layer 객체

    view와 control은 앱 컨텐츠 중 시각적인 부분을 제공
    
    view는 지정된 사각형 (frame)의 공간에 내용물을 그리고 그 프레임 안에 이벤트에 응답하는 객체이다
    
    control은 button, text field, toggle switch 와 같은 특정한 역활을 담당하는 view를 말한다
    
    UIKit Framework는 다양한 종류의 콘텐츠에 해당하는 기본 뷰들을 제공하고 있다
    
    UIView 또는 UIView의 서브클래스(button, label등)를 상속받아 커스텀 뷰를 작성할 수도 있다
    
    앱은 이런 view와 control을 포함하는 일 외에도, Core Animation layer를 view와 control외 계층에 포함시킬 수 있다
    
    layer 객체는 시각적 요소에 대한 Data 객체이다
    
    View는 Scene의 뒷부분에서 이 layer 객체를 사용하여 컨텐츠 내용을 나타낸다
    
    애니메이션이나 다른 시각적 효과를 보여주기 위해서 커스텀 layer 객체를 만들어 사용 할 수 있다
    
##### 하나의 iOS 앱은 앱이 관리하는 데이터 내용과 이 데이터를 표시하는 방법을 통해 다른 앱과의 차별점을 갖게 된다
##### UIKit 객체들간의 동작만으로 앱을 작동시킬 수는 없지만 그 작동에 많은 도움이 된다
##### 예를 들어, app delegate 메소드는 앱의 상태 변화를 체크하여 적절한 처리를 할 수 있도록 알려주는 역활을 한다

## iOS 앱 에서의 상태 변화

### 1. Not Running
    
    실행되지 않았거나, 시스템에 의해 종료된 상태
    
### 2. Inactive
    
    실행 중이지만 이벤트를 받고있지 않은 상태.
    
#### inactive 예시를 통한 설명

    앱 실행 중 미리알림 또는 일정 얼럿이 화면에 덮여서 앱이 실질적으로 이벤트를 받지 못하는 싱태
    
### 3. Active
    
    어플리케이션이 실질적으로 활동하고 있는 상태.

### Inactive와 Active 상태

    Inactive와 Active 상태는 앱의 상태 변화에 따라 혹은 상황에 따라 계속해서 상태의 변화가 이루어진다
    
    또한 Inactive와 Active 상태를 묶어 "Foreground" 라고 한다
    
### 3. Background
    
    백그라운드 상태에서 실질적인 동작을 하고 있는 상태
    
#### Background 예시를 통한 설명
    
    백그라운드에서 음악을 실행하거나, 걸어온 길을 트래킹 하는 등의 동작
    
### 4. Suspended

    백그라운드 상태에서 활동을 멍춘 상태
    
    빠른 재실행을 위하여 메모리에 적재된 상태이지만 실질적으로 동작하고 있지는 않다
    
    메모리가 부족할 때, 시스템이 강제종료하게 된다

### Image about State changes in iOS app

<img width="670" alt="applifestatus" src="https://user-images.githubusercontent.com/42841888/63157035-0927d480-c051-11e9-85a5-9e134ec7873e.png">