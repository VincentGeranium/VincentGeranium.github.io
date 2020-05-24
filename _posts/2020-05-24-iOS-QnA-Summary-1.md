---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 3 (App's Life Cycle, Scene-Based Life-Cycle, App-Based Life-Cycle Events)"
date:   2020-05-24
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Apple Documentation](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle)

- [뽀짝뽀짝들의 개발일지](https://jercy.tistory.com/11)

- [Vincent Blog - iOS 면접을 위한 문답 정리 - 2 (App Lifecycle 과 Methods)](https://vincentgeranium.github.io/ios,/swift/2020/05/23/iOS-QnA-Summary-1.html)

- - -
- - -

### Managing Your App's Life Cycle

- 앱이 foreground 나 background에 있을때 시스템 관련 이벤트를 처리한다.

- 개요
    
    - 앱의 현재 상태에 따라 언제든지 수행 할 수 있는 작업과, 수행 할 수 없는 작업이 결정된다.
    
    - 예를들어 foreground 상태의 앱은 유저가 보고 있는 화면이기에 CPU를 비롯한 시스템 리소스 우선순위가 높다.
    
    - 하지만 background 상태의 앱은 가능한 작은 작업을 해야하며, 화면이 안보이기에 아무것도 하지않는것이 좋다.
    
    - 앱 상태가 바뀌면 그에 따라 행동을 바꿔야 한다.
    
    - 앱의 상태가 바뀌면 UIKit은 적절한 delegate 메소드를 호출하여 사용자에게 알려준다.
    
- **iOS 13 이상에서는 UISceneDelegate를 사용하여 Scene 기반 라이프 사이클이 동작한다.**

- **iOS 12 이하에서는 UIApplicationDelegate에서 라이프 사이클이 동작한다.**

- **앱에서 Scene support를 설정하면 iOS 13 이상에서는 ScenDelegate를 항상 사용한다. iOS 12 이전 버전은 AppDelegate를 사용한다.**

- - -
- - -

### Respond to Scene-Based Life-Cycle Events

- 앱이 scene을 지원하면 UIKit은 각각에 대해 별도 라이프 사이클을 제공한다.

- scene은 기기에서 실행중인 앱 UI의 한 인스턴스를 나타낸다.

    - 유저는 각 앱에 대해 여러 scene을 만들고 이를 개별적으로 표시하거나 숨길 수 있다.
    
    - 각 scene마다 고유한 라이프 사이클이 있기 때문에 각 scene마다 다른 실행 상태가 될 수 있다.
    
        - 예를들어 한 scene이 foreground에 있고, 다른 scene은 background에 있거나 suspended 되었을 수 있다.
        
- **Scene은 선택적 기능이다.**

<img width="1058" alt="Scene-BasedLife-CycleEventsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/Scene-BasedLife-CycleEventsImage-1.png?raw=true" title="Scene-BasedLife-CycleEventsImage-1">

- 위 그림은 scene의 상태 전환을 보여주는 그림이다.

- 유저나 시스템이 앱의 새로운 scene을 요청하면 UIKit은 이를 생성하고 연결되지 않은 상태로 둔다.

    - 유저가 요청한 scene은 빠르게 foreground로 이동하여 화면에 나타난다.
    
    - 시스템이 요청한 scene은 background로 이동하여 이벤트를 처리한다.
    
        - 예를들어 시스템은 background에서 scene을 실행하여 location 이벤트를 처리할 수 있다.
        
- 유저가 앱을 닫으면 UIKit은 관련 scene을 background 상태로 이동, 결국 suspended 된다.

- UIKit은 리소스를 회수하기 위해 background나 suspended된 scene의 연결을 끊고 연결되지 않은 상태로 반환한다.

- - -
- - -

### Respond to App-Based Life-Cycle Events

- iOS 12 이전 버전이나 Scene을 지원하지 않는 앱에서 UIKit은 모든 라이프 사이클 이벤트를 UIApplicationDelegate로 전달한다.

- App delgate는 별도의 화면에 표시된 창을 포함하여 모든 앱의 창을 관리한다.

    - 따라서 앱 상태 전환은 앱의 전체 UI에 영향을 준다.
    
<img width="1058" alt="App-BasedLife-CycleEventsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/App-BasedLife-CycleEventsImage-1.png?raw=true" title="App-BasedLife-CycleEventsImage-1">

- 위 그림은 App delegate와 관련된 상태 전환을 보여주는 그림이다.

    - 앱 실행 후 UI가 화면에 표시 될지 여부에 따라서 시스템이 앱을 비활성 상태(Inactive) 또는 백그라운드 상태(Background)로 전환한다.
    
    - Foreground로 시작할 때 시스템은 앱을 자동으로 활성 상태(Active)로 전환한다.
    
    - 그 이후에 상태는 앱이 종료 될 때까지 활성(Active), 비활성(Inactive) 백그라운드(Background)로만 변한다.