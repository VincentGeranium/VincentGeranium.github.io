---
layout: post
title:  "앱 생명주기-2"
date:   2019-08-17
categories: Swift, iOS
---

## The Main Run Loop

    Main Run Loop는 사용자와 관련된 프로세스들을 처리한다.
    
    UIApplication 객체는 앱이 실행(lunch)되는 시점에 메인 run loop를 생성한 뒤
    
    run loop로 이벤트를 처리한다.
    
    Main run loop는 앱의 메인 스레드에서 동작한다.
    
    Main run loop는 사용자 관련 이벤트들을 받은 순서대로 처리한다.
    
## 앱에서의 main run loop와 사용자의 이벤트 인식 구조

<img width="670" alt="mainrunloop" src="https://user-images.githubusercontent.com/42841888/63214649-d0255800-c155-11e9-8463-3396f3c83918.png">

- 1. 사용자가 디바이스에서 특정 액션을 취한다

- 2. 그 액션에 해당하는 이벤트가 시스템에 의해 생성되어 UIKit에서 생성한 port를 통해 앱에 전달

- 3. 이벤트들은 앱 내부적으로 큐에 저장, 차례대로 해당 동작이 실행

- 4. UIApplication 객체가 가장 먼저 이 이벤트를 받아서 어떤 동작이 취해질지 결정

- 5. 터치 이벤트의 경우 main window 객체가 인식, window 객체가 다시 터치가 발생한 view로 이벤트를 전달

- 다른 이벤트들도 다양한 app 객체들에 따라 조금씩 다르게 작동한다.
    
    
    