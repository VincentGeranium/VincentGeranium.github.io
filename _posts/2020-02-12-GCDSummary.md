---
layout: post
title:  "Grand Central Dispatch Summary"
date:   2020-02-12
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - Grand Central Dispatch](https://www.edwith.org/boostcourse-ios/lecture/16916/)

- - -

### Grand Central Dispatch 한줄 요약

- `멀티코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술`

- - -

### Grand Central Dispatch (GCD)

- `Grand Central Dispatch(GCD)는 멀티코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술`

- 기본적으로 `스레드 풀의 관리`를 프로그래머가 아닌 `운영체제에서 관리`하기 때문에 `프로그래머가 태스크(작업)을 비동기적으로 쉽게 사용할 수 있다`

- `프로그래머가 실행할 태스크(작업)을 생성하고 Dispatch Queue에 추가하면 GCD는 태스크(작업)에 맞는 스레드를 자동으로 생성해서 실행하고 작업이 종료되면 해당 스레드를 제거한다`

- - -

### Dispatch Queue (디스패치 대기열)

![QueueImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/QueueImage-1.png?raw=true)

- `Dispatch Queue(디스패치 대기열)`은 `작업을 연속적 혹은 동시`에 `진행`하기는 하지만 `언제나 먼저 들어오면 먼저 나가는 순서로 실행된다(FIFO)`

#### Dispatch Queue (디스패치 대기열)의 종류

- 1) `Serial Dispatch Queue`는 `한 번에 하나의 작업만을 실행`, `해당 작업이 대기열`에서 `제외`되고 `새로운 작업이 시작되기 전`까지 `기다린다`

- 2) `Concurrent Dispatch Queue`는 `이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행한다`

- `Dispatch Queue`는 `GCD 기술의 일부이다`

- - -

### Dispatch Source (디스패치 소스)

- `Dispatch Source`는 `특정 유형의 시스템 이벤트`를 `비동기적으로 처리하기 위한 C 기반 메커니즘이다`

- `특정 유형의 시스템 이벤트에 대한 정보를 캡슐화`하고, `해당 이벤트가 발생할 때마다`, `특정 클로저(블록) 객체 혹은 기능`을 `Dispatch Queue에 전달`한다

- `Dispatch Source는 GCD 기술의 일부이다`

- - -

### Operation Queue (연산 대기열)

![QueueImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/QueueImage-2.png?raw=true)

- `Operation Queue(연산 대기열)`은 `Concurrent Dispatch Queue와 동일하게 동작`하며, `Operation Queue 클래스`에 의해 `구현`된다.

![QueueImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/QueueImage-3.png?raw=true)

- `Dispatch Queue(디스패치 대기열)`는 `항상 먼저 들어오면 먼저 나가는 순서(FIFO: First-In, First-Out)`로 `작업을 실행`하지만, `Operation Queue(연산 대기열)`은 `작업의 실행 순서를 결정할 때에 다른 요인들을 고려`한다.

- `Operation Queue(연산 대기열)`는 `Dispatch Queue(디스패치 대기열)와 매우 유사한 클래스`이다

- - -

### GCD와  Operation Queue (연산대기열)

#### 차이점

- Operation Queue에서는 동시에 실행 할 수 잇는 연산(Operation)의 최대 수를 지정할 수 있다.

- Operation Queue에서는 KVO(Key Value Observing)을 사용할 수 있는 많은 프로퍼티들이 있다.

- Operation Queue에서는 연산(Operation)을 일시 중지, 다시 시작 및 취소를 할 수 있다.

#### 언제 사용해야 할까?

- `Operation Queue`

    - 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는데 적합하다
    
    - KVO(Key Value Observing)을 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합하다
    
- `GCD`
    
    - 작업이 복잡하지 않고 간단하게 처리하거나 특적 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합하다. 예를 들면 타이머, 프로세스 등의 관련 이벤트.
    
- - -