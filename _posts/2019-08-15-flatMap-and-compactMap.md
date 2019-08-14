---
layout: post
title:  "flatMap and compactMap의 차이와 정리"
date:   2019-08-15
categories: Swift, iOS
---

# flatMap and compactMap

#### flatMap은 Deprecated (더 이상 사용되지 않음)
    swift 4.1 부터 compactMap으로 사용
    
    그러나 flatMap이 아에 사라지는 것은 아니다
    
#### flatMap과 compactMap은 쓰임에 따라서 구별해야 한다

<img width="570" alt="compactMap" src="https://user-images.githubusercontent.com/42841888/63033014-e4691b00-bef1-11e9-976f-4f8aa8fb2903.png">

<img width="570" alt="flatMap" src="https://user-images.githubusercontent.com/42841888/63033044-f480fa80-bef1-11e9-834d-f8888217cf71.png">

#### compactMap을 사용하는 상황 ??

    배열과 같이 squence에 nil에 매핑되는것들을 필터링 할 때
    
<img width="570" alt="compactMapExample" src="https://user-images.githubusercontent.com/42841888/63033455-96a0e280-bef2-11e9-8db5-d17817082f3a.png">

#### flatMap을 사용하는 상황 ??

- 1. 각 요소가 sequence일 때 평평하게 만들어준다

<img width="570" alt="flatmapExample1" src="https://user-images.githubusercontent.com/42841888/63033918-60179780-bef3-11e9-99d0-f51d4460a218.png">

- 2. optional에서 사용

<img width="570" alt="flatMapExample2" src="https://user-images.githubusercontent.com/42841888/63034209-d3b9a480-bef3-11e9-8471-0c24e142be7c.png">