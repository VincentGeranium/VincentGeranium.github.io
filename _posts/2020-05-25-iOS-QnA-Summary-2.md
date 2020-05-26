---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 4 (SceneDelegate, AppDelegate)"
date:   2020-05-25
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [레나참나](https://velog.io/@dev-lena/iOS-AppDelegate와-SceneDelegate)

- [ZeddiOS](https://zeddios.tistory.com/811)

- [usinuniverse](https://usinuniverse.bitbucket.io/blog/scenedelegatepart1.html)

- [Apple developer](https://developer.apple.com/videos/play/wwdc2019/258/)

- - -
- - -

### AppDelegate (iOS 12 and earlier)

<img width="1058" alt="AppDelegateImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AppDelegateImage-1.png?raw=true" title="AppDelegateImage-1">

- iOS 12 와 12 이전 버전에서는 AppDelegate 밖에 없다.

- iOS 12 와 12 이전 버전에서 AppDelegate의 역활은 크게 2가지로 나뉜다.

    - 1) Process Lifecycle
    
        - Process Lifecycle는 프로세스가 Launch되고, terminate 됐는지 알 수 있었다.
    
    - 2) UI Lifecycle
    
        - UI Lifecycle는 UI의 State를 알 수 있었다.
        
        - 아래와 같은 메소드들을 통해서 알 수 있었다.
        
```swift
application(_:didFinishLaunching:) // 앱이 처음 시작될 때 실행
        
applicationWillResignActive: // 앱이 active 에서 inactive로 이동될 때 실행 
        
applicationDidEnterBackground: // 앱이 background 상태일 때 실행 
        
applicationWillEnterForeground: // 앱이 background에서 foreground로 이동 될때 실행 (아직 foreground에서 실행중이진 않음)
        
applicationDidBecomeActive: // 앱이 active상태가 되어 실행 중일 때
        
applicationWillTerminate: // 앱이 종료될 때 실행
```

- 위의 메소드들은 iOS 12를 포함한 이전 버전까지는 사용 가능한 메소드였다.

    - 그 이유는  **앱은 오직 "하나의 프로세스와 그에 맞는 하나의 UI"만 가지기 때문이다.**
    
- - -
- - -

### AppDelegate와 SceneDelegate (iOS 13)

- **iOS 12 까지는 대부분 하나의 앱에 하나의 'window' 였지만 iOS 13 부터는 window의 개념이 'scene'으로 대체되었다.**

    - **window의 개념이 scene로 바뀌고(대체되고) 나서는 아래의 사진처럼 하나의 앱에서 여러개의 scene를 가질 수 있다.**
    
<img width="1058" alt="multiSceneImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/multiSceneImage-1.jpeg?raw=true" title="multiSceneImage-1">  

- AppDelegate의 역활 중 UI의 상태를 알 수 있는 UILifeCycle에 대한 부분을 'SceneDelegate'가 하게 되었다.

<img width="1058" alt="AppAndSceneDelegateImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AppAndSceneDelegateImage-1.png?raw=true" title="AppAndSceneDelegateImage-1">

- AppDelegate에 'Session Lifecycle'에 대한 역활이 추가 되었다.

    - Scene Session이 생성되거나 삭제될 때 AppDelegate에 알리는 두 메소드가 추가 되었다.
    
    - Scene Session은 앱에서 생성한 모든 scene의 정보를 관리한다.
    
<img width="1058" alt="AppDelegateMethodsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AppDelegateMethodsImage-1.png?raw=true" title="AppDelegateMethodsImage-1">

- iOS 13 부터 AppDelegate가 하는 책임(역활)이 달라진다.

<img width="1058" alt="SessionLifeCycle-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/SessionLifeCycle-1.png?raw=true" title="SessionLifeCycle-1">

- 이전에는 앱이 foreground에 들어가거나 background로 이동할 때 앱의 상태를 업데이트하는 등의 앱의 주요 생면 주기(App Lifecycle) 이벤트를 관리했었지만 더이상 하지 않는다.
    
- iOS 13 부터 AppDelegate가 하는 달라진 책임(역활)은 아래와 같이 구분할 수 있다.

    - 1) 앱의 가장 중요한 데이터 구조를 초기화하는 것
    
    - 2) 앱의 scene을 환경설정(Configuration)하는 것
    
    - 3) 앱 밖에서 발생한 알림(배터리 부족, 다운로드 완료 등)에 대응하는 것
    
    - 4) 특정한 scene, views, view controllers에 한정되지 않고 앱 자체를 타겟하는 이벤트에 대응하는 것.
    
    - 5) 애플 푸시 알림 서비스와 같이 실행시 요구되는 모든 서비스를 등록하는 것.
    
- AppDelegate 클래스는 새로운 프로젝트를 생성할 때마다 자동으로 생성된다.

    - 이 AppDelegate 클래스가 채택하고 있는 UIApplicationDelegate는 아래의 그림과 같은 메소드들이 있다.
    
    - 보통의 경우, 앱을 초기화하고 앱 레벨의 이벤트에 반응하기 위해서는 Xcode가 제공하는 이 클래스를 사용해야한다.
    
    - UIApplicationDelegate 프로토콜은 앱을 설정하고, 앱의 상태 변화에 대응하며, 다른 앱 레벨의 이벤트를 처리하는 데 사용하는 여러 메소드를 정의한다. 
    
<img width="1058" alt="UIApplicationDelegateImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIApplicationDelegateImage-1.png?raw=true" title="UIApplicationDelegateImage-1">    

- - -
- - -

### Scene

- **iOS 13 부터는 'window'의 개념이 'scene'으로 대체됐다.**

- UIKit은 UIWindowScene 객체를 사용하는 앱 UI의 각 인스턴스를 관리한다.

- Scene에는 UI 하나의 인스턴스를 나타내는 windows와 view controllers가 들어있다.

    - 또한 각 scene에 해당하는 UIWindowSceneDelegate 객체를 가지고 있다.
    
        - 이 객체는 UIKit과 앱 간의 상호 작용을 조정하는데 사용한다.
        
- Scene들은 같은 메모리와 앱 프로세스 공간을 공유하면서 서로 동시에 실행된다.

- 결과적으로 하나의 앱은 여러 scene와 scene delegate 객체를 동시에 활성화 할 수 있다.

- **UI의 상태를 알 수 있는 UILifeCycle에 대한 역활을 'SceneDelegate'가 하게 됐다.**

    - **역활이 분리된 대신 'AppDelegate'에서 Scene Session을 통해서 scene에 대한 정보를 업데이트 받는다.**
    
- - -
- - -

### Scene Session

- **UISceneSession 객체는 scene 고유의 런타임 인스턴스를 관리한다.**

    - 사용자가 앱에 새로운 scene을 추가하거나 프로그래밍적으로 scene을 요청하면, 시스템은 그 scene을 추적하는 session 객체를 생성한다.
    
        - 그 session에는 고유한 식별자와 scene의 구성 세부사항(configuration details)가 들어있다.
    
    - UIKit은 session 정보를 그 scene 자체의 생애(life time)동안 유지하고 app switcher에서 사용자가 그 scene을 클로징하는 것에 대응하여 그 session을 파괴한다.
    
        - session 객체는 직접 생성하지 않고 UIKit이 앱의 사용자 인터페이스에 대응하여 생성한다.
    
        - 또한 application(_:configurationForConnecting:option:) -> UISceneConfiguration 과 application(_:didDiscardSceneSessions:) 이 두 메소드를 통해 UIKit에 새로운 scene와 session을 프로그래밍적 방식으로 생성할 수 있다.
        
- - -
- - -