---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 7 (Dispatch Queue, Dispatch Source, Operation Queue, GCD와 OperationQueue의 차이점, Main Queue와 Global Queue, Dispatch Queue의 sync와 async 메소드)"
date:   2020-05-29
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [edwith](https://www.edwith.org/boostcourse-ios/lecture/16916/)

- [마기의 개발 블로그](https://magi82.github.io/gcd-01/)

- - -
- - -

### GCD

- Grand Central Dispatch (GCD)는 멀티코어와 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술.

    - 기본적으로 스레드 풀의 관리를 프로그래머가 아닌 운영체제에서 관리하기 때문에 프로그래머가 태스크(작업)을 비동기적으로 쉽게 사용할 수 있다.
    
    - 프로그래머가 실행할 태스크(작업)을 생성하고 Dispatch Queue에 추가하면 GCD는 태스크(작업)에 맞는 스레드를 자동으로 생성해서 실행하고 작업이 종료되면 해당 스레드를 제거한다.
    
    - 쉽고 편한 멀티 스레딩 처리를 위해 애플이 제공하는 API
    
        - GCD는 C기반의 저수준 API   

- - -
- - -

### Dispatch Queue (디스패치 대기열)

- Dispatch Queue는 작업을 연속적 혹은 동시에 진행하기는 하지만, FIFO(First-In, First-Out)로 언제나 먼저 들어오면 먼저 나가는 순서로 실행된다.

- 실제로 해야할 Task(작업)을 담아두면 선택된 스레드에서 실행을 해주는 역활을 한다.

#### Dispatch Queue의 종류

<img width="1058" alt="serialImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/serialImage-1.png?raw=true" title="serialImage-1">

- Serial Dispatch Queue는 한 번에 하나의 작업만 실행하며, 해당 작업이 대기열에서 제외되고 새로운 작업이 시작되기 전까지 기다린다.

<img width="1058" alt="concurrentImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/concurrentImage-1.png?raw=true" title="concurrentImage-1">

- Concurrent Dispatch Queue는 이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행한다.

- Dispatch Queue(디스패치 대기열)은 GCD 기술 일부이다.

#### Main Queue와 Global Queue

- 앱 실행시 시스템에서 기본적으로 2개의 Queue를 만들어 준다.

    - Main Queue와 Global Queue
    
- Main Queue

    - **메인 스레드(UI 스레드)에서 사용되는 Serial Queue이다.**
    
    - 모든 UI 처리는 메인 스레드에서 처리를 해야한다.
    
- Global Queue

    - **편의상 사용할 수 있게 만들어 놓은 Concurrent Queue이다.**
    
    - Global Queue는 처리 우선 순위를 위한 qos(Quality of service) 파라미터를 제공한다.
    
    - 병렬적으로 동시에 처리를 하기 때문에 작업 완료의 순서는 정할 수 없지만 우선적으로 일을 처리하게 할 수 있다.
    
    - qos의 우선순위는 아래와 같다.
    
        - 1) userInteractive
        
        - 2) userInitiated
        
        - 3) default
        
        - 4) utillity
        
        - 5) background
        
        - 6) unspecified

- - -
- - -

#### Dispatch Queue의 sync와 async 메소드

- **sync는 동기 처리 메소드이다.**

    - 해당 작업을 처리하는 동안 다음으로 진행되지 않고 계속 머물러 있다.
    
- **async는 비동기 처리 메소드이다.**    

    - sync와는 다르게 처리를 하라고 지시 후 다음으로 넘어간다.
    
- 보통 스레드 처리를 하는 작업들은 시간이 꽤나 걸리는 큰 작업이거나 언제 끝날지 모르는 알 수 없는 작업에 사용된다. 예를 들어 네트워크, 파일로딩 등.
    
    - **작업이 처리되는 동안에 아무것도 하지 못하고 멈춰있으면 앱이 렉이 걸리거나 아무 반응이 없는것처럼 보인다.**
    
    - **그래서 보통 동기 처리 메소드인 sync는 잘 사용하지 않는다.**
    
- **Serial / Concurrent와 sync / async 는 별개이다.**

    - 직렬인데 비동기 일 수도 있고, 병렬인데 동기 일 수도 있다.
    
    - 직렬과 병렬은 한 번에 하나만 처리하느냐 동시에 여러 개 처리하느냐에 따라 구분지어지는 것이다.
    
    - 동기와 비동기는 처리가 끝날 때까지 기다리느냐 지시만 하고 다른 처리를 하느냐에 따라 구분 지어지는 것이다.

- - -
- - -

#### Dispatch Source (디스패치 소스)

- Dispatch Source는 특정 유형의 시스템 이벤트를 비동기적으로 처리하기 위한 C 기반 메커니즘.

- 특정 유형의 시스템 이벤트에 대해 정보를 캡슐화하고, 해당 이벤트가 발생할 때마다 특정 클로저(블록) 객체 혹은 기능을 DispatchQueue(디스패치 대기열)에 전달한다.

- Dispatch Source는 GCD 기술 일부이다.

- - -
- - -

#### Operation Queue(연산 대기열)

- Operation Queue(연산 대기열)은 Concurrent Dispatch Queue와 동일하게 동작하며, Operation Queue 클래스에 의해 구현된다.

- Dispatch Queue(디스패치 대기열)와 동일하게 동작하며, Operation Queue 클래스에 의해 구현된다.

- Dispatch Queue(디스패치 대기열)은 항상 먼저 들어오면 먼저 나가는 순서(FIFO)로 작업을 실행하지만, Operation Queue(연산 대기열)은 작업의 순서를 결정할 때에 다른 요인들을 고려한다.

- Operation Queue(연산 대기열)은 Dispatch Queue(디스패치 대기열)과 매우 유사한 클래스이다.

- - -
- - -

### GCD와 Operation Queue(연산 대기열)의 차이점

- Operation Queue에서는 동시에 실행할 수 있는 연산(Operation)의 최대 수를 지정할 수 있다.

- Operation Queue에서는 KVO(Key Value Observing)을 사용할 수 있는 많은 프로퍼티들이 있다.

- Operation Queue에서는 연산(Operation)을 일시 중지, 다시 시작 및 취소를 할 수 있다.

- - -
- - -

### 단어 정리

- Process

    - 하나의 프로그램이 메모리에서 실행되는 작업단위.
    
    - 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램을 말한다.
    
    - 종종 스케줄링의 대상이 되는 작업(task)이라는 용어와 거의 같은 의미로 쓰인다.
    
- 멀티 코어(Multi-Core)

    - 멀티 코어 또는 멀티 코어 프로세서(Multi-core processor) CPU는 두 개 이상의 독립 코어를 단일 직접 회로로 이루어진 하나의 패키지로 통합한 것이다.
    
- Task(작업)

    - 스케줄링의 대상이 되는 작업.
    
- 멀티 프로세싱(Multi-Processing), 다중 처리

    - 컴퓨터 시스템 한 대에 둘 이상의 CPU(중앙 처리 장치)를 이용하여 병렬로 처리하는 것을 가리킨다.
    
    - 이 용어는 하나 이상의 프로세서를 지원하는 시스템의 능력, 또는 이들 사이의 태스크를 할당하는 능력을 가리키기도 한다.
    
- 다중 처리 시스템(Multiprocessing System)

    - 다중 처리가 적용된 시스템을 뜻한다.
    
    - 다중 처리 시스템에서는 여러 개의 프로세서가 하나의 메모리를 공유하여 사용하는 시스템이며, 일반적으로 하나의 운영 체제가 모든 프로세서들을 제어한다.