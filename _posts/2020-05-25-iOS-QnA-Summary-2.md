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

- - -
- - -

### AppDelegate (iOS 12 and earlier)

<img width="1058" alt="AppDelegateImage-1" src="" title="AppDelegateImage-1">

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

### AppDelegate (iOS 13)

- iOS 13 부터는 앱은 여전히 하나의 프로세스를 공유하지만, 여러 UI 인스턴스 또는 Scene session이 있을 수 있기 때문이다.

- - -
- - -


### Scene?

- 



- - -
- - -




### AppDelegate와 SceneDelegate

- **iOS 12 까지는 대부분 하나의 앱에 하나의 'window' 였지만 iOS 13 부터는 window의 개념이 'scene'으로 대체되었다.**

    - **window의 개념이 scene로 바뀌고(대체되고) 나서는 아래의 사진처럼 하나의 앱에서 여러개의 scene를 가질 수 있다.**
    
<img width="1058" alt="multiSceneImage-1" src="" title="multiSceneImage-1">    
