---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 6 ()"
date:   2020-05-28
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [아이군의 블로그](http://theeye.pe.kr/archives/2470)

- - -
- - -

### NSOperataionQueue

- NSOperationQueue는 작업의 동시 실행을 조절하는 일을 한다.

- 이 큐는 우선순위 큐와 같이 동작하며 기본적으로 First-In-First-Out으로, 동작을 하나 더 높은 우선 순위(NSOperation.queuePriority)의 작업이 들어오게 되면 더 낮은 우선 순위를 가진 작업들을 건너뛰고 실행한다.

- NSOperationQueue는 maxConcurrentOperationCount 프로퍼티 설정을 이용해 주어진 특성 시간동안 동시에 실행 가능한 작업의 숫자를 제한하는것이 가능하다.

- NSOperation을 시작하기 위해서는 start 메소드를 호출하거나 NSOperationQueue에 추가하여 큐의 가장 처음에 도달하면 한번 실행되도록 할 수 있다.

- NSOperation을 사용하여 얻을 수 있는 많은 장점들이 NSOperationQueue를 사용함에서 오기 때문에 NSOperation의 start를 직접적으로 호출하는것보다는 NSOperationQueue에 추가하여 사용하는것이 바람직하다.

- - -
- - -