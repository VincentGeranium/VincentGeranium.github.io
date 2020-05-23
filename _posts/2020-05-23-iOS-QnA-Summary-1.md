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
        
### UIApplication

- UIApplication의 정의 "The centralized point of control and coordination for apps running in iOS."

    - 모든 앱에는 UIApplication 인스턴스가 하나만 있다. (매우 드물게 UIApplication의 하위 클래스)

    - 앱이 시작되면, 시스템은 UIApplicationMain 함수를 호출한다
    
```swift
func UIApplicationMain(_ argc: Int32, 
                     _ argv: UnsafeMutablePointer<UnsafeMutablePointer<Int8>?>, 
                     _ principalClassName: String?, 
                     _ delegateClassName: String?) -> Int32
```

- iOS 앱들은 UIApplicationMain 함수를 실행한다. 이 때 생성되는 것 중 하나가 UIApplication 객체이다.

    - UIApplication 객체는 Singleton 형태로 생성, UIApplication.shared의 형태로 앱 전역에서 사용할 수 있다.
    
    - UIApplication 객체는 Event Loop에서 발생하는 여러가지 이벤트들을 감지하고 Delegate에 전달하는 역활.
        
        - 예를 들어 앱이 background로 갈 때, 메모리 부족 경고를 할 때와 같은 상황들을 감지하여 Delegate에 전달한다.
        
- AppDelegate 객체는 UIApplication 객체로 부터 메시지를 받았을 때, 해당 상황에서 실행될 함수들을 정의한다.

    - Xcode로 Swift 프로젝트를 만들면 자동으로 생성되는 AppDelegate.swift 파일이 있는데 이 파일이 AppDelegate 객체가 된다. 그 이유는 클래스 선언부에 @UIApplicationMain 어노테이션이 붙어 있는것을 볼 수 있다.
    
        - 즉, 앱이 구동되면 AppDelegate.swift의 AppDelegate 클래스를 델리게이트 객체로 지정한다.
        
        - AppDelegate 객체에는 앱의 상태에 따라 실행되는 함수들이 정의되어 있다.

### Main Event Loop

- Main Event Loop 라는 것은 유저가 일으키는 이벤트들을 처리하는 프로세스이다.
    
<img width="1058" alt="MainRunLoopImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/MainRunLoopImage-1.PNG?raw=true" title="MainRunLoopImage-1">    

- 유저가 일으키는 이벤트의 처리 과정 순서

    - 1). 유저가 이벤트를 일으킨다.
    
    - 2). 시스템을 통해 이벤트가 생성된다.
    
    - 3). UIKit Framework를 통해 생성된 port로 해당 이벤트가 앱으로 전달.
    
    - 4). 이벤트는 앱 내부적으로 Queue의 형태로 정리되고, Main Run Loop에 하나씩 Mapping 된다.
    
    - 5). UIApplication 객체는 이때 가장 먼저 이벤트를 받는 객체로 어떤 것이 실행돼야 하는지 결정한다.