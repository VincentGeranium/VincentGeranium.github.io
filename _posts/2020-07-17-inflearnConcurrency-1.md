---
layout: post
title:  "Inflearn - iOS Concurrency Programming 강의 정리 노트"
date:   2020-07-17
categories: iOS, Swift
---

이 포스트는 앨런(Allen)님의 강의 중 "iOS Concurrency(동시성) 프로그래밍, 동기 비동기 처리 그리고 GCD/Operation - 디스패치큐와 오퍼레이션큐의 이해" 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

#### 참고 자료

[앨런(Allen)님의 강의 "iOS Concurrency(동시성) 프로그래밍, 동기 비동기 처리 그리고 GCD/Operation - 디스패치큐와 오퍼레이션큐의 이해"](https://www.inflearn.com/course/iOS-Concurrency-GCD-Operation#)

- - -
- - -

### 섹션 0

- - -
- - -

#### 간단한 GCD / Operation 소개

- iOS에서 대기행렬을 "Queue" 또는 "대기열"이라고 표현하며 크게 두 가지로 나뉨.

    - 1) GCD(Grand Central Dispatch) - Dispatch Queue
    
    - 2) Operation - Operation Queue
        
        - 작업 자체로는 Operation 라고 표현.
        
- GCD / Operation        

    - 직접적으로 스레드 관리 X, "Queue를 만들어 작업을 분산 처리."

        - Queue(대기열/대기행렬) 안에 Tasks(작업들)을 넣어주기만 하면 iOS(Operation System)이 알아서 스레드를 생성하여 작업을 분배, 분산 처리한다.
    
    - GCD / Operation 을 사용하여 "시스템에서 알아서 스레드 숫자를 관리한다."

        - 직접 스레드를 관리, 생성하는 것은 하드웨어나 일의 부하(load)와 같은 시스템에 대한 지식이 없이 사용시 오히려 앱이 느려질 수 있음.
    
    - 스레드 보다 더 높은 레벨/차원에서 일을 한다고 보면 됨.

    - 쉽게 다른 스레드에서 (오래 걸리는)작업들이 "비동기적으로 동작"하도록 만들어 줌.
        
        - 어떤 API들은 내부적으로 다른 스레드에서 비동기적으로 실행되도록 설계되어 있음.
        
- - -
- - -

#### Queue에 보내는 방법

```swift
// Code Example
DispatchQueue.global().async {
    // 작업 코드
    // 즉, 다른 스레드로 보낼 작업을 배치
}
```

- 위 예시 코드는 "글로벌 큐에 비동기적으로 작업을 보내겠다."라는 뜻이다.

    - 이 DispatchQueue 클로저 안에 들어가는 것은 "작업의 한 단위 이다."
    
    - 즉, "{ }" 이 괄호 안에 들어가는 것이 "작업의 한 단위."
    
        - 만약 작업이 2개이면 DispatchQueue로 보내는 코드가 2개가 되어야 한다. 한 괄호 안에 모든 작업을 넣어주면 X.
        
```swift
// 작업 당 DispatchQueue로 보내는 코드 예시

DispatchQueue.global().async {
    task 1
}

DispatchQueue.global().async {
    task 2
}
```

- 작업의 단위 == "하나의 클로저" 안에 보내는 작업 자체가 묶이는 개념.

    - 작업의 단위가 중요한 이유는 한 클로저 안에 작업(task)에 관한 여러 중간 과정의 작업들이 있다고 가정하면 "하나의 클로저" 안에 묶여있는 작업들이니 모두 순서대로 이루어 진다.
    
        - 비동기적으로 작업을 처리하는 큐 안에 여러 줄의 코드가 써있다고 비동기적으로 중간 과정이 먼저 끝나는 중간 과정 작업의 순서대로 끝나는것이 아니고 하나의 클로저 안에 묶여있는 작업이므로 코드의 순서대로 작업이 처리되는 것이다.

- - -
- - -

#### GCD 와 Operation 의 차이점 (간략하게 설명)

- GCD (Grand Central Dispatch)

    -  = Dispatch Queue.

    - 간단한 일 (커뮤니케이션의 양).
        
        - 클로저로 묶을 수 있는 간단한 작업양
        
    - 함수를 사용하는 작업 (메서드 위주).
    
- Operation

    - = Operation Queue.
    
    - 복잡한 일 (커뮤니케이션의 양).
    
    - 데이터와 기능을 캡슐화한 객체.
    
    - GCD를 기반으로 만들어진 기술.
    
        - GCD 기술 + 여러가지 기능 (취소 / 순서지정 / 일시중지(상태추적))
        
        - 2016년에 APPLE에서 발표한 기술.
        
        - GCD 에서 발전된 기술이라고 생각하면 됨.
        
- - -
- - -

#### 마무리

- GCD 또는 Operation 중 한 가지를 꼭 써야한다. 뭐가 더 중요하고 두 가지 중 이게 좋다 낫다 라는 개념은 없다.

    - 다만 프로젝트의 효율성과 적합성 등을 고려해 사용해야 한다.
    
    - 각각의 장단점 그리고 프로젝트의 적합성플 파악해 GCD를 사용할지 Operation을 사용할지 선택하면 된다.
    
    - 다만 Operation 은 Class 이기 때문에 Class 로 만들어 놓으면 재사용하기 편하다.

- - -
- - -
