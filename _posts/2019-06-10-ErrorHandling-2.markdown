---
layout: post
title:  "Error Handling (2)"
date:   2019-06-10
categories: iOS, Swift
---

### 참고 자료

이 포스트는 yagom's Swift Basic을 참고하여 쓴 포스트임을 미리 밝힙니다

[야곰님 블로그로 가기](https://yagom.github.io/swift_basic/contents/21_error_handling/)

아래의 링크는 현재 포스트와 내용이 이어지는 Error Handling(1)로 가는 링크 입니다

[Vincent의 Error Handling(1)](https://vincentgeranium.github.io/ios,/swift/2019/06/07/ErrorHandling.html)

아래의 링크는 현재 포스트를 바탕으로 한 실습 구현 자료로 가는 링크 입니다
[vincent의 Error Handling 구현](https://github.com/VincentGeranium/Swift-Study/tree/master/ErrorHandling-2.playground)

---

# Error Handling(2)

---

## Error throw from the originated Error Function (함수에서 발생한 오류 던지기)

![exampleImage](https://user-images.githubusercontent.com/42841888/59169348-ef5fa200-8b74-11e9-8864-d0647a4bfb8c.png)

- 위 사진은 자판기 동작 도중 발생한 오류를 던지는 메서드를 구현 한 것입니다.

- 오류 발생 여지가 있는 메서드는 `throws`를 사용하여 오류를 내포하는 함수임을 표시

---

## Error Process (오류처리)

**오류를 던질 수도 있지만 오류가 던져지는 것에 대비하여 던져진 오류를 처리하기 위한 코드도 작성되어야 한다**

- 예를 들어,
    - 던져진 오류가 무엇인지 판단하여 다시 문제를 해결
    - 다른 방법으로 시도
    - 사용자에게 오류를 알리고 사용자에게 선택 권한을 넘겨주어 어떤 동작을 하게 할 것인지 결정하도록 유도

**오류 발생의 여지가 있는 `throws` 함수(메서드)는 `try`를 사용하여 호출해야 함**

---

## Error Process (do - catch)

**오류 발생의 여지가 있는 `throws` 함수(메서드)는 `do - catch` 구문을 활용하여 오류 발생에 대비해야 함**

- 가장 정석적인 방법
    - 모든 오류 케이스에 대응
    
![image1](https://user-images.githubusercontent.com/42841888/59176270-83d8fd00-8b93-11e9-9ec3-63e7b53e58d0.png)

- 하나의 catch 블럭에서 switch 구문을 사용하여 오류를 분류
    - 위의 그림에 나오는 것과 크게 다를것이 없음
    
![image2](https://user-images.githubusercontent.com/42841888/59176296-92271900-8b93-11e9-9b4f-8a69fd468a8f.png)

- 딱히 케이스별로 오류처리 할 필요가 없으면 catch 구문 내부를 간략화해도 무방

![image3](https://user-images.githubusercontent.com/42841888/59176325-a23ef880-8b93-11e9-89e5-309b05e263a0.png)

---

## Error Process (try? , try!)

**try?**

별도의 오류처리 결과를 통보받지 않고 오류가 발생시 결과값을 nil로 돌려받을 수 있다

정상동작 후에는 옵셔널 타입으로 정상 반환값을 돌려 받는다

![image4](https://user-images.githubusercontent.com/42841888/59176347-be429a00-8b93-11e9-907a-e343026a625d.png)

**try!**

오류가 발생하지 않을 것이라는 확신이 있을때 try! 사용

정상동작 후에는 바로 결과값을 돌려받는다

오류 발생시 런타임 오류가 발생, 애플리케이션 동작이 중지됨

![image5](https://user-images.githubusercontent.com/42841888/59176357-c8649880-8b93-11e9-9f2f-5ef7173c66a6.png)
