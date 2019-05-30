---
layout: post
title:  "guard 문과 if 문의 차이"
date:   2019-05-30
categories: iOS, Swift
---

# guard and if syntax

---

### 참고 자료

이 포스트는 Out of Bedlam님의 블로그 포스트 중 "스위프트 guard의 활용"을 참고하여 쓴 포스트임을 미리 밝힙니다

[Out of Bedlam님의 블로그](https://outofbedlam.github.io/swift/2016/03/04/guard/)

---

## guard 문

guard문과 if문의 용도는 확실히 구별되며, 그 용도에 맞게 사용하는 것이 코드를 짜거나, 가독성에도 좋다

guard 문은 뭔가를 검사하여 그 다음에 오는 코드들을 실행할지 말지 결정

guard 문에 주어진 조건문이 거짓이 될 때에 코드 블럭이 실행

### 예시코드

- is 10

![is_10](https://user-images.githubusercontent.com/42841888/58601886-b6e2dd00-82c5-11e9-80af-68300384d09b.png)

- not 10

![not_10](https://user-images.githubusercontent.com/42841888/58602048-530ce400-82c6-11e9-9ba9-e36e6648a23b.png)

---

## guard 와 if 의 차이점

if 문을 사용해서도 동일하게 함수의 파라미터나 실행 전제 조건들을 검사하도록 할 수 있지만,

**guard의 경우**에는 **조건식에 이 함수가 수행하는데 필요한 조건을 그대로 나타낸다는 점**에서 **if문에서 부정적인 조건식으로 표현**하는 것보다 **가독성이 높아**진다는 장점이 있다
