---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 9 (NotificationCenter 동작 방식과 활용, Notification)"
date:   2020-05-31
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Apple Docs - Notification](https://developer.apple.com/documentation/foundation/notification)

- [Apple Docs - NotificationCenter](https://developer.apple.com/documentation/foundation/notificationcenter)

- [edwith](https://www.edwith.org/boostcourse-ios/lecture/16919/)

- [얄미대디, 개발과 투자](https://m.blog.naver.com/jdub7138/220937372865)

- - -
- - -

### Notification Center와 Notification

<img width="1058" alt="notiAndnotiCenterImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/notiAndnotiCenterImage-1.png?raw=true" title="notiAndnotiCenterImage-1">

#### Notification

- **노티피케이션 센터를 통해 등록된 모든 옵저버에게 정보를 브로드캐스트(뿌려주는)하는 컨테이너.**

- 등록된 노티피케이션에 노티피케이션 센터를 통해 정보를 전달하기 위한 구조체.

- Notification 주요 프로퍼티

    - name : 알림을 식별하는 태그
    
    ```swift
    var name: Notification.Name
    ```
    
    - object : 발송자가 옵저버에게 보내려고 하는 객체. 주로 발송자 객체를 전달하는 데 쓰임
    
    ```swift
    var objcet: Any?
    ```
    
    - userInfo : 노티피케이션과 관련된 값 또는 객체의 저장소
    
    ```swift
    var userInfo: [AnyHashable:Any]?
    ```
    
    - 특정 행동으로 인해 작업이 시작되거나 완료되는 시점에 다른 인스턴스로 노티피케이션이 발생 시 필요한 데이터를 같이 넘겨줄 수 있다.
    
        - 예를 들어 네트워킹을 이용하는 애플리케이션이라면 네트워킹이 시작 및 완료되는 시점, 음악 및 동영상 재생 등에도 재생이 끝나는 시점에 관련된 정보를 넘겨 줄 수 있다.

#### NotificationCenter

- **등록된 옵저버에 정보를 브로드캐스트(뿌릴 수있는) 노티피케이션 발송 메커니즘.**

- 등록된 옵저버에게 동시에 노티피케이션을 전달하는 클래스이다.

    - NotificationCenter 클래스는 Notificaiton을 발송하면 Notification Center에서 메세지를 전달할 Observer의 처리가 완료될 때까지 대기한다.
    
        - **즉, 흐름이 동기적(synchronous)으로 흘러간다.**
        
        - Notification을 비동기적(Asynchronous)으로 사용하려면 NotificationQueue를 사용하면 된다.
        
- **기본 NotificationCenter 얻기**

    - default : 애플리케이션의 기본 노티피케이션 센터이다.
    
    ```swift
    class var `default`: NotificationCenter {get}
    ```

- **옵저버 추가 및 제거**

    - addObserver(forName:object:queue:using:) : 노티피케이션을 노티피케이션 대기열(Queue)과 대기열(Queue)에 추가 할 블록(Swift의 Closure), 노티피케이션 이름을 노티피케이션 센터의 메서드를 가리키는 장소(디스패치 테이블, Dispatch Table)에 이름을 추가한다. 여기서 object에 특정 객체를 명시하면 명시한 객체가 발송한 노티피케이션일 때에만 해당 이름의 노티피케이션을 수신한다.
    
    ```swift
    func addObserver(
        forName name: NSNotification.Name?, 
        object obj: Any?, 
        queue: OperationQueue?, 
        using block: @escaping (Notification) -> Void) -> NSObjectProtocol
    ```
    
    - addObserver(_:selector:name:object:) : 노티피케이션을 노티피케이션 센터의 메서드를 가리키는 장소에 이름을 추가한다.
    
    ```swift
    func addObserver(
        _ observer: Any,
        selector aSelector: Selector,
        name aName: NSNotification.Name?
        object anObject: Any?)
    ```
    
    - removeObserver(_:name:object:) : 노티피케이션 센터의 메서드를 가리키는 장소에서 일치하는 이름을 제거한다.
    
    ```swift
    func removeObserver(
        _ observer: Any,
        name aName: NSNotification.Name?,
        object anObject: Any?)
    ```
    
    - removeObserver(_:) : 노티피케이션 센터의 메서드를 가리키는 장소에서 모든 이름을 제거한다.
    
    ```swift
    func removeObserver(_ observer: Any)
    ```

- **노티피케이션 발송**

    - post(_:) : 지정된 노티피케이션을 노티피케이션 센터에 발송한다.
    
    ```swift
    func post(_ notification: NOtification)
    ```
    
    - post(name:object:userInfo:) : 지정된 이름, 보낸 객체, 보낼 정보로 노티피케이션을 만들어 노티피케이션 센터에 발송한다.
    
    ```swift
    func post(
        name aName: NSNotification.Name,
        object anObject: Any?,
        userInfo aUserInfo: [AnyHashable : Any]? = nil)
    ```
    
    - post(name:object:) : 지정된 이름, 보낸 객체로 노티피케이션을 만들어 노티피케이션 센터에 발송한다.
    
    ```swift
    func post(name aName: NSNotification.Name, object anObject: Any?)
    ```

- - -
- - -

### 객체간 소통 - Notification

- **iOS에서 객체들끼리 교신하는 대표적인 방법으로는 Callback, Notification, Delegate 이렇게 3가지가 있다.**

    - 객체 인스턴스를 만드는 방식도 있지만 그것보다는 이 세가지 방법이 더 효율적인 경우가 많다.
    
#### 뒷단의 작업이 완료되는 순간 파악하기

- **프로그래밍과 관련된 중급 주제 중 가장 많이 다루어지는 것이 바로 Multi-threading과 Asynchronous Programming 이다.**

    - 간단히 말하자면 멀티스레딩이란 여러 작업들이 동시(Concurrent)에 진행되는 것을 말하며, Async란 다른 작업을 기다리거나 방해하지 않고 바로 자신의 작업을 진행하는 프로그래밍을 말한다.
    
- **Multi-therading 및 Async에서 중요한 것은 뒷단에서 돌기 있는 함수가 완료되는 순간을 인지하는 것이다.**

    - 예를 들어, 용량이 큰 이미지를 불러오는 어떤 함수가 있다고 하자, 이 함수는 사용자 인터페이스 흐름을 막지 않기 위해 main queue가 아닌 global queue에서 Async(비동기적)으로 수행된다.
    
        - 이 때, 이미지를 불러오기 작업이 완료되는 이벤트가 발생하면 이를 인지하고 작업을 처리해주어야 한다.
        
        - 이러한 완료 이벤트 인지 작업과 관련하여 Swift에서는 Callback, Notification, Delegate 3가지 방법이 존재한다.
        
#### Notification을 통해 인지하기

- **Notification은 한 객체가 다른 객체에 자신의 업데이트 상태를 알려주는 방법 중 하나이다.**

    - **방식은 instance-to-instance communication으로서 라디오 센터처럼 전파를 쏘아주는 구조로 이루어진다.**
    
    - Notification을 통해 화면에 키보드가 나타나거나, 데이터 다운로딩이 완료되는 것과 같이 **어떤 작업이 완료되거나 특정 이벤트가 발생할 경우 이를 다른 객체들에게 알려줄 수 있다.**
    
    - 이러한 Notificaion은 **프로그래밍 디자인 패턴 중 Observation 패턴 중 하나로서 MVC 구조에서 Model이 Controller에게 말을 걸기 위해 사용하는 방식이기도 하다.**
    
- Mulit-threading 그리고 Async와 관련하여 뒷단에서 작업을 하는 인스턴스가 자신이 수행하는 작업을 완료하면 Notificcation을 통해 자신의 채널을 듣고 있는 인스턴스들에게 이를 통보할 수 있다.

    - Loop을 통해 변화가 있나 없나 계속 듣고 있어야 하기 때문에 Callback closure에 비해 자원적인 측면에서는 비효율적일 수도 있다.
    
        - **그러나 한 객체의 변화를 여러 객체들이 관찰해야 하는 경우 등에서는 Notification 방식이 다른 방법보다 나을 수 있다.**
        
#### Notification

- 여기서 말하는 Notification은 Push Notification과는 다른 의미이다.

    - Notification은 자신의 메세지를 받기로 한 가입객체에게 메세지를 보내게 된다. 이때 메세지를 보내는 객체는 자신의 가입객체에 대해 알 수 없고 그저 메세지만 보내게 된다.
    
    - 애플에서 직접 만든 코드 중 이 Notification이 활용되는 대표적인 사례는 앱에 키보드가 등장하는지 파악하더나, 홈버튼이 눌려 앱이 백그라운드로 이동했는지 파악하는 Notification을 꼽을 수 있다.
        