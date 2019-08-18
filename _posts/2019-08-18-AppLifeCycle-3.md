---
layout: post
title:  "앱 생명주기-3"
date:   2019-08-18
categories: Swift, iOS
---

## 앱 상태 변화에 따른 AppDelegate 메소드 호출과 처리

- application:willFinishLaunchingWithOptions : 앱을 실행할 때 최초로 실행할 코드를 작성하면 좋다

- application:didFinishLauchingWithOptions: 앱의 화면이 사용자에게 보여지기 직전에 최종 초기화 작업을 진행 할 수 있다

- applicationDidBecomeActive: 앱이 Foreground로 갈 것이라고 알려준다. 최종 준비 작업을 하면 된다

- applicationWillResignActive: 앱이 Foreground에서 다른 상태로 전환이 될 것임을 알려준다

- applicationDidEnterBackground: 앱이 Background에서 돌아가게 될 것임을 알려준다. 언제든지 Suspended 상태로 변환이 될 수 있다

- applicationWillEnterForeground: 앱이 Background에서 다시 Foreground로 돌아오게 될 것임을 얼려준다 그러나 아직 앱이 Active 상태는 아니다

- applicationWillTerminate: 앱이 종료될 것임을 알려준다. 만약 앱이 Suspended 상태라면 이 메소드는 호출 되지 않는다.

## App Termination

    앱은 언제든지 종료될 수 있기 때문에 항상 앱 종료에 대한 대비를 하여 사용자 데이터를 저장하거나 크리티컬한 작업을 수행 할 수 있어야 한다.
    
    시스템에서 앱을 종료시키는 건 앱의 Life Cycle에 따라 자연스러운 부분이다.
    
    시스템은 주로 다른 앱을 위한 메모리 확보를 위해 앱을 종료시키게 된다
    
    하지만 시스템은 앱의 오작동이나 이벤트에 적절한 대처가 없을 경우에도 종료를 시키게 된다
    
    Suspended 상태의 앱은 앱이 종료될 때 (시스템이 프로세스를 kill 하고 메로미를 확보하기 위함)
    
    어떤 알림도 받지 못한다.
    
    하지만 만약 앱이 Background에서 돌아가고 있어 Suspended 상태가 아니라면 시스템은 앱을 종료시키기 전에
    
    "applicationWillTerminate:" 메소드를 호출하게 된다.
    
    디바이스를 재부팅 할 때는 이 메소드를 호출하지 않는다.
    
    시스템이 앱을 종료시키는 것 외에도, 사용자가 Multitasking UI를 사용하여 앱을 종료시킬 수 있다
    
    사용자가 앱을 종료시킬 때는 Suspended 상태의 앱을 종료시키는 것과 같은 효과를 갖게 된다
    
    앱은 죽게되고 앱 종료에 대한 알림은 전달되지 않는다.
    
## Threads and Concurrency

    시스템은 앱의 메인 스레드를 만든다.
    
    "개발자들 또한 여러 작업을 수행하기 위해 필요한 만큼 추가적인 스레드를 생성 할 수 있다"
    
    iOS에서 멀티스레드를 위해 주로 사용하는 방법은 "GCD(Grand Central Dispatch), Operation Objects, 비동기 programming interfaces"이다
    
    개발자가 직접 스레드를 생성하여 관리하는 것은 지양하고 있다
    
    GCD와 같은 기술은 개발자들이 수행하고자 하는 작업을 원하는 순서대로 정의 할 수 있는 방법을 제공한다
    
    동시에 시스템에게 사용가능한 CPU자원으로 최선의 작업 수행을 하는 방법을 선택하도록 한다
    
    "시스템에게 이러한 스레드 관리를 맡김으로써 개발자가 작성해야 할 코드는 더욱 간결해진다"
    
## Threads and Concurrency 고려 할 점

- View와 관련된 작업, Core Animation, 그리고 다양한 UIKit 클래스들에 대한 작업은 무조건 앱의 Main 스레드에서 이루어져야 한다
    - 예외 : 예를 들어 이미지에 기반한 작업은 Background 스레드에서 수행 될 수 있다, 하지만 조금이라도 의심이 간다면 그냥 Main 스레드에서 작업을 하는 것으로 생각하면 된다

- 규모가 큰 작업(또는 길어질 수도 있는 작업)은 Background 스레드에서 진행해야 한다. 네트위크 접근, 파일 접근, 대용량 데이터들에 대한 처리들을 포함하는 작업은 GCD 또는 Operation 객체를 통해 Background 스레드에서 이루어지도록 해야한다

- 앱 실행시에는 가능한 많은 작업들을 Main 스레드에서 빼줘야 한다. 앱이 런치되는 시간에 앱은 최대한 빨리 UI를 셋팅하는데 집중해야 한다. 따라서 앱의 UI셋팅에 필요한 작업들만 Main 스레드에 포함시키도록 해야한다. 다른 작업들은 비동기로 수행되어 완료가 되는 시점에 사용자에게 보여지도록 하는 방법을 사용해야 한다