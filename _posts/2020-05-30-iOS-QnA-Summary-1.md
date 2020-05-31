---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 8 (Processor, Core, 프로그램(Program)과 프로세스(Process), Thread, 비동기(Asynchronous) 프로그래밍, 동시성(Concurrency) 프로그래밍, 병렬성(Parallelism) 프로그래밍, 동시성(Concurrency)과 병렬성(Parallelism) 차이, iOS 환경 동시성 프로그래밍 지원 종류)"
date:   2020-05-30
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [wiki - thread](https://ko.wikipedia.org/wiki/스레드_(컴퓨팅))

- [wiki - process](https://ko.wikipedia.org/wiki/프로세스)

- [edwith](https://www.edwith.org/boostcourse-ios/lecture/16866/)

- - -
- - -

### 프로세서 (Processor)

- **프로세서는 하드웨어적인 측면에서 컴퓨터 내에서 프로그램을 수행하는 하드웨어 유닛이다.**

    - **대표적으로 중앙처리장치(Central Processing Unit - CPU)가 이에 속한다.**
    
    - 한 컴퓨터가 여러 개의 프로세서를 갖는다면 멀티 프로세서라고 말한다. 듀얼 프로세서라고 한다면 한 컴퓨터에 두 개의 프로세서가 운용된다고 할 수 있다.
    
#### 코어 (Core)

- **프로세서에서 코어는 주요 연산회로이다.**

    - 싱글코어는 말 그대로 하나의 연산회로가 내장되어 있는 것이고 듀얼코어는 두 개의 연산회로가 내장된 것을 뜻한다.
    
    - **또, 여러 개의 코어를 가진 프로세서를 멀티 프로세서라고 한다.**
    
#### 프로그램(Program)과 프로세스(Process)

- 프로그램은 일반적으로 보조기억 장치(하드 디스크, CD 등.)에 저장된 실행코드이다.

    - 즉, 생명이 없는 상태.
    
- **프로세스는 프로그램을 구동하여 프로그램 자체와 프로그램 상태가 메모리상에서 실행되는 작업 단위를 말한다.**

    - **동시에 여러 개의 프로세스를 운용하는 시분할 방식을 멀티태스킹(Multitasking)이라고 한다.**
    
    - 이러한 프로세스 관리는 운영체제에서 담당한다.
    
- **프로세스는 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램을 말한다.**
    
    - 종종 스케줄링의 대상이 되는 작업(task)이라는 용어와 거의 같은 의미로 쓰인다.
    
    - **여러 개의 프로세서를 사용하는 것을 멀티프로세싱(Multiprocessing)이라고 한다.**
    
#### 스레드 (Thread)

- **스레드는 하나의 프로세스 내에서 실행되는 작업흐름의 단위를 말한다.**

    - 보통 한 프로세스는 하나의 스레드를 가지고 있지만, 프로세스 환경에 따라 둘 이상의 스레드를 동시에 실행할 수 있다. 이러한 방식을 멀티스레딩(Multithreading)이라고 한다.
    
    - **프로그램 실행이 시작될 때부터 동작하는 스레드를 메인 스레드라고 한다.**
    
        - **그 외에 나중에 생성된 스레드를 서브 스레드 또는 세컨더리 스레드라고 한다.**
        
<img width="1058" alt="MultithreadedImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/MultithreadedImg-1.png?raw=true" title="MultithreadedImg-1">


#### 비동기(Asynchronous) 프로그래밍

- **프로그램의 주 실행 흐름을 멈추어서 기다리는 부분 없이 바로 다음 작업을 실행할 수 있게 하는 방식.**

    - **즉, 코드의 실행 결과처리를 별도의 공간에 맡겨둔 뒤 결과를 기다리지 않고 바로 다음 코드를 실행하는 병렬처리 방식.**
    
    - 비동기 프로그래밍은 언어 및 프레임워크에서 지원하는 여러 방법으로 구현할 수 있다.
    
#### 동시성(Concurrency) 프로그래밍

- **논리적인 용어로 동시에 실행되는 것처럼 보이는 것이다.**

    - **싱글 코어(멀티 코어에서도 가능)에서 멀티스레드를 동작시키기 위한 방식으로 멀티 태스킹을 위해 여러 개의 스레드가 번갈아 가면서 실행되는 방식이다.**
    
    - **동시성을 이용한 싱글 코어의 멀티 태스킹은 각 스레드들이 병렬적으로 실행되는 것처럼 보이지만 사실은 서로 번갈아 가면서 실행되고 있는 방식이다.**

<img width="1058" alt="ConcurrencyImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ConcurrencyImg-1.jpeg?raw=true" title="ConcurrencyImg-1">

#### 병렬성(Parallelism) 프로그래밍

- **물리적으로 정확히 동시에 실행되는 것을 말한다.**

    - **멀티 코어에서 멀티 스레드를 동작시키는 방식으로 데이터 병렬성(Data Parallelism)과 작업 병렬성(Task Parallelism)으로 구분된다.**
    
<img width="1058" alt="parallelismImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/parallelismImage-1.png?raw=true" title="parallelismImage-1">    
    
- **데이터 병렬성(Data Parallelism) : 전체 데이터를 나누어 서브 데이터들로 만든 뒤, 서브 데이터들을 병렬 처리해서 작업을 빠르게 수행하는 방법.**

- **작업 병렬성(Taks Parallelism) : 서로 다른 작업을 병렬 처리하는 것을 말한다.**

#### 동시성(Concurrency)과 병렬성(Parallelism) 차이

- **동시성 프로그래밍(Concurrency Programming)과 병렬성 프로그래밍(Parallelism Programming) 모두 비동기(Asynchronous) 동작을 구현할 수 있지만, 그 동작 원리가 다르다.**

    - 동시성(Concurrency) : 통장을 만들러 온 N개의 대기열과 한 명 싱상의 은행직원.
    
    - 병렬성(Parallelism) : 통장을 만들어 온 N개의 대기열과 N명의 은행직원.
    
<img width="1058" alt="bankerImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/bankerImage-1.png?raw=true" title="bankerImage-1">

- 동시성의 개념은 논리적이며 병렬성의 개념은 물리적이다.

- 동시성의 동작 가능 환경은 싱글 코어, 멀티 코어가 가능하지만 병렬성은 멀티 코어만 가능하다.

    - 즉, 동시성은 싱글 코어 및 멀티 코어에서 모두 구현할 수 있지만, 병렬성은 멀티 코어에서만 구현할 수 있다.
    
#### iOS 환경 동시성 프로그래밍 지원 종류

- **Grand Central Dispatch (GCD) : 멀티 코어와  멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술**

- **Operation Queue (연산 대기열) : 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용한다.**

- **Thread : 멀티스레드 프로그래밍을 위한 애플에서 제공하는 스레드 클래스이다.**

- - -
- - -