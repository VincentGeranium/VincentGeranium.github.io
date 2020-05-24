---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 2 (App Lifecycle 과 Methods)"
date:   2020-05-23
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Eth Dev Post](https://hcn1519.github.io/articles/2017-09/ios_app_lifeCycle)

- [zedd iOS](https://zeddios.tistory.com/539)

- [young kim blog](https://medium.com/ios-development-with-swift/앱-생명주기-app-lifecycle-vs-뷰-생명주기-view-lifecycle-in-ios-336ae00d1855)

- [Apple Documentation](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle)

- - -
- - -

### App Lifecycle 과 Methods

- C언어 기반의 프로그램에서는 main 이라는 함수가 앱의 시작이 된다.

    - iOS 는 Objective-C 기반 , Objective-C는 C언어 기반이다.
    
    - 그러므로 iOS 앱은 main 함수에서 시작하지만, iOS의 핵심 라이브러리인 UIKit framework가 main 함수를 관리하여 개발자들이 직접 main 함수에 코드를 작성하지 않는다.
    
    - 그렇다고 개발자가 관여할 수 없는 것은 아니다. UIKit은 main 함수를 다루는 과정에서 UIApplicationMain 함수를 실행한다. 이 함수를 통해 UIApplication 객체가 생성되는데 이 객체를 통해 개발자는 앱의 실행에 부분적으로 관여할 수 있따.
    
    - 개발자가 앱을 실행하고 그 앱에 여러가지로 관여할 때 접근할 수 있는 객체가 UIApplication이다.
    
- 앱 생명주기 (App Lifecycle)는 홈버튼을 눌렀을 때, 전화가 왔을 때와 같이 앱이 화면상에서 보이지 않는 background 상태, 화면에 올라와 있는 상태인 foreground 등과 같은 상태들을 정의한 것 이다.

    - 앱 아이콘을 눌러 앱을 실행시키면 아래와 같은 일들이 일어난다.
        
        - UIApplication 객체를 생성.
        
        - @UIApplicationMain 어노테이션이 있는 클래스를 찾아 AppDelegate 객체를 생성.
        
        - Main Event Loop를 실행 (touch, text input등 유저의 액션을 받는 루프) 및 기타 설정.
        
- - -
- - -        
        
### UIApplication

- UIApplication의 정의 "The centralized point of control and coordination for apps running in iOS."

    - 모든 앱에는 UIApplication 인스턴스가 하나만 있다. (매우 드물게 UIApplication의 하위 클래스)

- 앱이 시작되면, 시스템은 UIApplicationMain 함수를 호출한다.

    - 이 함수는 다른 task들 중에서 싱글톤(Singleton) UIApplication 객체를 만든다. 그 후 shared 클래스 메소드를 호출하여 객체에 접근한다.

```swift
@available(iOS 2.0, *)
open class UIApplication : UIResponder {
    open class var shared: UIApplication { get }
}    
```

- 즉, 앱 시작시 UIApplicataionMain 함수가 shared app instance를 만든다.

- UIApplicationMain 함수는 application 객체와 application delegate를 만들고, 이벤트 사이클을 설정하는 역활을 가지고 있다.

```swift
func UIApplicationMain(_ argc: Int32, 
                     _ argv: UnsafeMutablePointer<UnsafeMutablePointer<Int8>?>, 
                     _ principalClassName: String?, 
                     _ delegateClassName: String?) -> Int32
```

- argc: argc의 개수, 대게 main에 해당하는 파라미터.

- argv: argument의 변수 목록. 대게 main에 해당하는 파라미터.

- principalClassName: UIApplication 클래스 또는 하위 클래스의 이름. nil을 지정하면, UIApplication으로 가정된다.

- delegateClassNAme: application delegate가 인스턴스화 되는 클래스의 이름이다. prinsipalClassName이 UIApplication의 하위클래스를 지정하는 경우, 하위 클래스를 delegate로 지정 할 수 있다. 하위클래스 인스턴스는 앱의 delegate 메세지를 받는다. 앱의 기본 nib 파일에서 delegate 객체를 로드하는 경우, nil을 지정한다.

- application 객체의 주요 역활은, 들어오는 사용자 이벤트의 초기 라우팅을 처리하는 것이다.

    - 컨트롤 객체(UIControl의 인스턴스)가 적절한 target 객체에 전달한 action 메세지를 전달한다.
    
- application 객체는 열린 window(UIWindow의 객체)의 목록을 유지관리하며, 이를 통해 앱의 UIView 객체를 검색할 수 있다.

- UIApplication 클래스는 UIApplicationDelegate 프로토콜을 준수하고, 일부 프로토콜 메소드를 구현해야하는 delegate를 정의한다.

    - application 객체는 delegate에게 중요한 런타임 이벤트(예: 앱 시작, 메모리 부족 경고 및 앱 종료)를 알리고, 적절히 응답 할 기회를 제공한다.
    
- 대부분의 앱은 UIApplication을 서브클래싱 할 필요가 없다.

    - 대신 add delegate를 사용하여 시스템과 앱 간의 상호작용을 관리하면 된다.
    
    - 앱에 들어오는 이벤트를 시스템이 처리하기 전에 처리해야하는 경우(매우 드문경우) 사용자 정의 이벤트 또는 디스패칭 메커니즘을 구현 할 수 있다.
    
        - 위와 같이 하려면 UIApplication을 서브클래스화 하고, sendEvent 와/또는 sendAction 메소드를 override 해야한다.
        
        - 인터셉트하는 모든 이벤트에 대해 이벤트를 처리 한 후, [super sendEvent:event]를 호출하여 시스템에 이벤트를 다시 전달해야 한다.
        
        - 이벤트를 가로채는 것은 거의 필요하지 않으며, 가능한 피해야한다.
        
```swift
@available(iOS 2.0, *)
open class UIApplication : UIResponder {

    open class var shared: UIApplication { get }
    
    unowned(unsafe) open var delegate: UIApplicationDelegate?
}    
```

<img width="1058" alt="UIApplicationImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIApplicationImage-1.png?raw=true" title="UIApplicationImage-1">

- 즉, 앱이 시작되는 순간, main에서 UIApplictionMain 함수가 application 객체를 만들고, delegate도 만든다.

- Objc에서는 main.mdptj UIApplication 함수를 호출햇지만, Swift에서는 appDelegate.swift에서 AppDelegate 클래스 앞에 어노테이션으로 붙은 @UIApplicationMain을 통해 UIApplicationMain을 호출한다.

```swift
import UIKit
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {...}
```

- UIApplicationMain 에 파라미터가 여러개 있었는데, 가장 마지막에 delegateClassName 은 AppDelegate에서 UIApplicationMain 함수를 호출했으니, 이 delegateClassName에 "AppDelegate"라는 이름을 전달한것과 동일하다.

    - 그리고, AppDelegate 클래스의 인스턴스를 만들고, 이 인스턴스를 위에서 만든 application 객체에 할당한다.
    
        - 즉, 지금 appDelegate와 application 객체가 연결된 것.
        
        - 그리고 application 객체가 delegate 메소드인 application:didFinishLaunchingWothOptions: 를 호출하게 된다.
        
        - 그러면 지금 AppDelegate 객체가 UIApplicationDelegate를 채택하고 준수하고 있으니, 여기에 있는 application:didFinishLaunchingWithOptions: 가 호출되게 되고 이제 앱이 실행된다.
        
- 위에서 AppDelegate의 인스턴스는 앱의 콘텐츠가 그려질 window를 만드는 역활을 한다고 했다. 그래서 앱을 시작하면, 하얀화면이 뜨게 되는 것.

    - window 객체가 이벤트를 처리 할 수 없는 경우, 이벤트는 singleton app object(application 객체의 shared)로 전달된다.
    
    - application 객체가 이벤트를 처리 할 수 없는 경우, 이벤트를 삭제한다.
    
- - -
- - -    
    
### AppDelegate 의 앱 상태애 따라 실행되는 함수.    
    
- **AppDelegate.swift 에는 앱 상태에 따라 실행되는 delegate 함수들이 정의 되어 있다.**

    - **이 함수안에 코드를 작성 함으로써 앱이 특정 상태에 동작하는 로직을 작성할 수 있다.**

        - application(_:didFinishLaunching:) - 앱이 처음 시작될 때 실행
        
        - applicationWillResignActive: - 앱이 active 에서 inactive로 이동될 때 실행 
        
        - applicationDidEnterBackground: - 앱이 background 상태일 때 실행 
        
        - applicationWillEnterForeground: - 앱이 background에서 foreground로 이동 될때 실행 (아직 foreground에서 실행중이진 않음)
        
        - applicationDidBecomeActive: - 앱이 active상태가 되어 실행 중일 때
        
        - applicationWillTerminate: - 앱이 종료될 때 실행
        
- 위 함수를 모두 구현할 필요는 없다. 상황에 맞춰 필요한 함수만 구현하면 된다. 혹은 위 함수들에는 없지만 원하는 delegate 를 추가할 수도 있다.

- - -
- - -

### Main Event Loop

- Main Event Loop 라는 것은 유저가 일으키는 이벤트들을 처리하는 프로세스이다.
    
<img width="1058" alt="MainRunLoopImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/MainRunLoopImage-1.PNG?raw=true" title="MainRunLoopImage-1">    

- 유저가 일으키는 이벤트의 처리 과정 순서

    - 1). 유저가 이벤트를 일으킨다.
    
    - 2). 시스템을 통해 이벤트가 생성된다.
    
    - 3). UIKit Framework를 통해 생성된 port로 해당 이벤트가 앱으로 전달.
    
    - 4). 이벤트는 앱 내부적으로 Queue의 형태로 정리되고, Main Run Loop에 하나씩 Mapping 된다.
    
    - 5). UIApplication 객체는 이때 가장 먼저 이벤트를 받는 객체로 어떤 것이 실행돼야 하는지 결정한다.
    
- - -
- - -

### App State(앱 상태)

- 앱 상태는 크게 5가지로 구분된다.

<img width="1058" alt="AppStateImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AppStateImage-1.PNG?raw=true" title="AppStateImage-1">

    - Not Running : 앱이 실행되지 않은 상태.
    
    - Inactive : 앱이 실행중이지만 아무런 이벤트를 받지 않는 상태, 앱의 상태 전환 과정에서 잠깐 머무는 단계
    
    - active : 앱이 실행중인 상태, 이벤트를 받는 상태.
    
        - Inactive + active = Foreground 상태
        
    - background : 앱이 백그라운드에 있는 상태, 실행되는 코드가 있는 상태. 앱이 suspended(유예 상태) 상태로 진입하기 전 거치는 상태.
    
    - suspeneded : 앱이 백그라운드에 있고, 실행되는 코드가 없는 상태. 시스템이 임의로 background 상태의 앱을 suspended 상태로 만든다.
    
- 앱 상태에서 알아두면 좋은 몇가지가 있다.

    - 1). Background 상태에서는 일부 필요한 추가 작업을 수행할 수 있다
    
        - 또한, Background 상태에서 앱을 실행하면 InActive 상태를 거치지 않고 앱이 실행된다.(iOS 에서 홈 버튼을 두 번 눌러서 앱을 전환할 때, 앱이 재시작되지 않는다면 해당 앱은 Background 상태에 있던 앱이다.)
        
    - 2). 앱이 죽는 것(Suspended 상태에서 Not Running 상태로 진입하는 것)에는 알림을 받을 수 없다.
    
        - 또한, Background 상태에서 Suspended 상태로 진입 할 떄 willTerminate 메소드가 실행되지만 이 또한 기기를 재부팅하면 실행되지 않는다.
        
- - -
- - -

### Respond to Scene-Based Life-Cycle Events

<img width="1058" alt="Scene-BasedLife-CycleEventsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/Scene-BasedLife-CycleEventsImage-1.png?raw=true" title="Scene-BasedLife-CycleEventsImage-1">

- - -
- - -

### Respond to App-Based Life-Cycle Events

<img width="1058" alt="App-BasedLife-CycleEventsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/App-BasedLife-CycleEventsImage-1.png?raw=true" title="App-BasedLife-CycleEventsImage-1">

- - -
- - -