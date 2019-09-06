---
layout: post
title:  "When to Use Threads (Concurrency Programming Guide)"
date:   2019-09-06
categories: iOS, Swift, CS
---

## [Concurrency Programming Guide - 1](https://vincentgeranium.github.io/ios,/swift,/cs/2019/08/31/CPG.html)

## [Concurrency Programming Guide - 2](https://vincentgeranium.github.io/ios,/swift,/cs/2019/09/04/CPG.html)

## [Concurrency Programming Guide - 3](https://vincentgeranium.github.io/ios,/swift,/cs/2019/09/06/CPG.html)

---

# When to Use Threads

- operation queues와 dispatch queues는 task를 동시에 수행하는 기본 방법이지만, 모든것을 해결할 수 있는 방법은 아니다

- 앱에 따라 사용자 정의 쓰레드를 만들어야 할 때가 있을 수 있다

- 커스텀 쓰레드를 만드는 경우, 가능한 적은 수의 쓰레드를 생성하려고 노력해야 한다.

- 다른 방법으로는 구현할 수 없는 특정 task에만 쓰레드를 사용해야 한다

- 쓰레드는 실시간으로 실행해야하는 코드를 구현하는 좋은 방법이다

-dispatch queues는 가능한 빨리 task를 실행하려고 시도하지만, 실시간 제약조건을 처리하지는 않는다

- 백그라운드에서 실행되는 코드에서보다 예측가능한 동작이 필요한 경우 쓰레드가 여전히 더 나은 대안을 제공 할 수 있다

- 다른 쓰레드 프로그래밍과 마찬가지로 절대적으로 필요한 경우에만 항상 쓰레드를 적절하게 사용해야 한다

- 쓰레드 사용방법에 대한 자세한 내용은 [Apple Document about Threading Programming Guide]를 참고.(https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/Introduction/Introduction.html#//apple_ref/doc/uid/10000057i)

---

참고 자료

- [Apple Document about Threading Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/Introduction/Introduction.html#//apple_ref/doc/uid/10000057i)

- [Apple Developer Document about CPG](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091-CH1-SW1)

- [Apple Developer Document about OpenCL](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/OpenCL_MacProgGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008312)

- [ZeddiOS](https://zeddios.tistory.com/509)