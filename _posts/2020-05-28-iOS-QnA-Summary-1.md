---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 6 (NSOperataionQueue, NSOperation)"
date:   2020-05-28
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [아이군의 블로그](http://theeye.pe.kr/archives/2470)

- [Seorenn SIGSEGV](http://seorenn.blogspot.com/2014/06/swift-nsoperationqueue.html)

- - -
- - -

### NSOperataionQueue

- NSOperationQueue는 작업의 동시 실행을 조절하는 일을 한다.

- 이 큐는 우선순위 큐와 같이 동작하며 기본적으로 First-In-First-Out으로, 동작을 하나 더 높은 우선 순위(NSOperation.queuePriority)의 작업이 들어오게 되면 더 낮은 우선 순위를 가진 작업들을 건너뛰고 실행한다.

- NSOperationQueue는 maxConcurrentOperationCount 프로퍼티 설정을 이용해 주어진 특성 시간동안 동시에 실행 가능한 작업의 숫자를 제한하는것이 가능하다.

- NSOperation을 시작하기 위해서는 start 메소드를 호출하거나 NSOperationQueue에 추가하여 큐의 가장 처음에 도달하면 한번 실행되도록 할 수 있다.

- NSOperation을 사용하여 얻을 수 있는 많은 장점들이 NSOperationQueue를 사용함에서 오기 때문에 NSOperation의 start를 직접적으로 호출하는것보다는 NSOperationQueue에 추가하여 사용하는것이 바람직하다.

- NSOperationQueue는 큐에 작업을 쌓아두고 이 작업들을 병렬로 처리하기 위한 클래스이다.

    - Queue라고 해서 한번에 하나씩 처리가 될 거라고 생각될 수도 있지만, 개별 작업을 개별 쓰레드에서 가능한 만큼 병렬로 한번에 실행한다.

- - -
- - -

### NSOperation

- 이 클래스는 OperationQueue에 넣기 위한 단위 클래스이다.

    - 즉 모든 작업은 이 NSOperation 타입의 클래스로 구현되어야 한다.
    
    - 다만 기본적으로 이 클래스는 추상 클래스에 가까워서 단일로는 아무일도 하지 않고 상속해서 구현하는 형태로 사용해야한다.
    
- NSOperation은 어떤 하나의 작업을 나타낸다.

- NSOperation은 모델링 상태, 우선순위, 의존성 그리고 관리를 지원하는 유용한 Thread safe한 추상 클래스이다.

- - -
- - -