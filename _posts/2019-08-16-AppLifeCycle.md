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


    

앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있고, 상태 변화에 따라 다른 동작을 처리하기 위한 델리게이트 메서드들을 설명하시오.