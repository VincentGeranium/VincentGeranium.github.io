---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 : (맵, 필터, 리듀스(Map, Filter, Reduce) - 맵, 필터, 리듀스의 활용)"
date:   2020-06-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Map, Filter, Reduce Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-MapFilterReduceExampleCode-1.playground)

- - -
- - -

### 맵, 필터, 리듀스의 활용

- 아래 두 코드는 맵, 필터, 리듀스를 통합하여 사용해 목록의 친구들을 특정 조건으로 분류하여 콘솔에 출력하는 예제이다.

<img width="1058" alt="mapFilterReduceImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapFilterReduceImage-1.png?raw=true" title="mapFilterReduceImage-1">

- 먼저 위의 코드에서는 친구들의 정보를 담을 수 있는 구조체 Friend와 성별을 나타내는 열거형 Gender를 정의하고 친구들의 정보를 담아둘 배열 friends를 생성했다.

    - 하지만 위 코드에 입력된 자료는 작년 자료이다. 그래서 친구들의 나이는 실제 나이보다 한 살 더 적게 기입되어 있다.
    
    - 일단 이 점을 기본 전제로 조건에 맞는 친구를 찾을 예정이다. 조건은 "풀럼 외의 지역에 거주하며 25세 이상인 친구"이다.
    
<img width="1058" alt="mapFilterReduceImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapFilterReduceImage-2.png?raw=true" title="mapFilterReduceImage-2">

- 위 코드를 살펴보면, 먼저 맵으로 나이를 한 살씩 더해 새 Friend 배열을 생성해준다.

- 그리고 필터로 풀럼에 사는 친구들과 25세 미만인 친구들을 걸러 낸 후, 리듀스로 필터링한 후 변형된 자료를 원하는 모양으로 합쳐서 출력했다.

- - -
- - -