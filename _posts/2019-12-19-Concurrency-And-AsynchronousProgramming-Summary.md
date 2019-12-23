---
layout: post
title:  "동시성 프로그래밍, 비동기성 프로그래밍, 병렬성 프로그래밍"
date:   2019-12-19
categories: iOS, Swift, CS
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 동시성 프로그래밍, 병렬성 프로그래밍과 비동기 프로그래밍](https://www.edwith.org/boostcourse-ios/lecture/16866/)

- - -

### 동시성 프로그래밍, 병렬성 프로그래밍, 비동기 프로그래밍

- 처음부터 이 모든 개념을 상세히 이해하기 어렵다

- `서로의 개념이 완전히 별도의 개념도 아니고, 그렇다고 같은 개념도 아니다, 조금씩 얽혀있는 개념들이다`

- - -

### 이해를 돕기 위한 간단한 정의

- 동기적 일처리 방식 : `순차적`으로 일을 스스로 `끝내 나가는` 방식

- 비동기적 일처리 방식 : 해야 할 일을 `위임`하고 `기다리는` 방식

- - -

### 프로세서

- 프로세서 : 하드웨어적인 측면에서 컴퓨터 내에서 프로그램을 수행하는 하드웨어 유닛

- 대표적으로 중앙처리장치(Central Processing Unit - CPU)가 이에 속함

- 멀티 프로세서 : 한 컴퓨터가 여러 개의 프로세서가 운용되는것

- 듀얼 프로세서 : 한 컴퓨터에 두 개의 프로세서가 운용되는것

- - -

### 코어

- 프로세서에서 코어는 주요 연산회로이다.

- 싱글 코어 : 말 그대로 하나의 연산회로가 내장되어있는것

- 듀얼 코어 : 두 개의 연산회로가 내장된 것을 뜻함

- 멀티 코어 프로세서 : 여러 개의 코어를 가진 프로세서

- - -

### 프로그램과 프로세스 (Program and Process)

- `프로그램`은 일반적으로 보조기억 장치에 저장된 실행코드 즉, 생명이 없는 상태를 말한다

- `프로세스`는 프로그램을 구동하여 프로그램 자체와 프로그램의 상태가 메모리상에서 실행되는 작업 단위를 말한다

- 동시에 여러 개의 프로세스를 운용하는 시분할 방식을 `멀티태스킹`이라고 한다

- `이러한 프로세스 관리는 운영체제에서 담당한다`

- - -

### 스레드(Thread)

- `스레드는 하나의 프로세스 내에서 실행되는 작업흐름의 단위`

- 보통 한 프로세스는 하나의 스레드를 갖고있다

- 프로세스 환경에 따라 둘 이상의 스레드를 동시에 실행할 수 있다

    - `이러한 방식을 멀티스레딩이라고 한다`
    
- 프로그램 실행이 시작될 때부터 동작하는 스레드를 `메인 스레드`라고 하고 그 이외에 나중에 생성된 스레드를 `서브 스레드` 또는 `세컨터리 스레드`라고 한다.

![ThreadImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ThreadImage.png?raw=true)

- - -

### 비동기 프로그래밍 (Asynchronous Programming)

- `프로그램의 주 실행 흐름을 멈추어서 기다리는 부분 없이 바로 다음 작업을 실행할 수 있게 하는 방식`

- 즉, 코드의 실행 결과처리를 별도의 공간에 맡겨둔 뒤 결과를 기다리지 않고 바로 다음 코드를 실행하는 `병렬처리 방식`

- 비동기 프로그래밍은 언어 및 프레임워크에서 지원하는 여러 방법으로 구현할 수 있다.

- - -

### 동시성 프로그래밍 (Concurrency Programming)

- 논리적인 용어로 동시에 실행되는 것 처럼 보이는 것이다

- `싱글 코어(멀티 코어에서도 가능)에서 멀티스레드를 동작시키키 위한 방식`

    - `멀티 태스킹을 위해 여러 개의 스레드가 번갈아 가면서 실행되는 방식`
    
- `동시성`을 이용한 `싱글 코어의 멀티 태스킹`은 각 스레드들이 `병렬적`으로 실행되는 것 처럼 보이지만 `사실은 서로 번갈아 가면서 실행되고 있는 방식`이다

![ConcurrencyImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ConcurrencyImage.png?raw=true)

- - -

### 병렬성 프로그래밍 (Parallelism Programming)

- `물리적으로 동시에 정확히 동시에 실행되는 것을 말한다`

- `멀티 코어`에서 `멀티 스레드를 동작시키는 방식`으로 `1) 데이터 병렬성(Data Parallelism)`과 `2) 작업 병렬성(Task Parallelism)`으로 `구분`된다

- - -

#### 데이터 병렬성 (Data Parallelism)

- `전체 데이터를 나누어 서브 데이터들로 만든 뒤, 서브 데이터들을 병렬 처리해서 작업을 빠르게 수행하는 방법`

![DataParallelismImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/DataParallelismImage.png?raw=true)

#### 작업 병렬성 (Task Parallelism)

- `서로 다른 작업을 병렬 처리하는 것을 말한다`

![TaskParallelismImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TaskParallelismImage.png?raw=true)

- - -

### 동시성(Concurrency)과 병렬성(Parallelism)의 차이

- 동시성 프로그래밍과 병렬성 프로그래밍 모두 비동기(Asynchronous)동작을 구현할 수 있지만, 그 동작 원리가 다르다

    - 동시성(Concurrency) : 통장을 만들러 온 N개의 대기열과 한 명 이상의 은행직원
    
    - 병렬성(Parallelism) : 통장을 만들어 온 N개의 대기열과 N명의 은행직원


![ConcurrencyAndParallelismImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ConcurrencyAndParallelismImage.png?raw=true)

![ConcurrencyAndParallelismImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ConcurrencyAndParallelismImage-2.png?raw=true)

- `즉, 동시성은 싱글코어 및 멀티코어에서 모두 구현할 수 있지만, 병렬성은 멀티 코어에서만 구현할 수 있다`

- - -

### iOS 환경 동시성 프로그래밍 지원 종류

- Grand Central Dispatch (GCD) : 멀티 코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술

- Operation Queue (연산 대기열) : 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용

- Thread : 멀티스레드 프로그래밍을 위한 애플에서 제공하는 스레드 클래스
