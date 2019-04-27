---
layout: post
title:  "열거형(Enum) 문제 풀이"
date:   2019-04-27
categories: iOS, Swift
---

# Enumeration

---

오늘은 시험 문제 중 Enumeration에 관한 문제를 풀어보려 합니다.

문제를 한번 보시죠!!

문제는 다음과 같습니다

```
 구글(google), 카카오(kakao), 네이버(naver) 로그인을 위해 Site라는 이름의 Enum 타입을 만들고자 합니다.
 각 case는 사용자의 아이디(String)와 비밀번호(String)를 위한 연관 값(associated value)을  가집니다.
 그리고 Site 타입 내부에는 signIn()이라는 이름의 메서드를 만들어 다음과 같이 문자열을 출력하는 기능을 구현해보세요.
 
 e.g.
 enum Site {}
 > Input
 let google = Site.google("google@gmail.com", "0000")
 google.signIn()
 
 > Output
 구글에 로그인하였습니다. (아이디 - google@gmail.com, 비밀번호 - 0000)
```

저는 처음에 enum에 대한 `명확한 개념`을 갖고 있지 않았어요.

그래서 enum이 뭔지 먼저 구글링을 통해 알아봤죠

Enumeration(enum) 은 유사한 종류의 여러값을 유의미한 이름으로 한곳에 모아 정의한 것 이라고 볼 수 있디고 해요.

즉, 열거형 자체가 `하나의 데이터 타입`인것이죠.

열거형은 `케이스 하나 하나가 고유한 의미`를 나타낼 수 있다고 해요.

열거형이 어떤 것인지 알아봤으니 문제 풀이 해설로 돌아가 볼까요??

저는 처음 저 문제를 접하고 나서 엄청 막막했어요

```
enum Site {
    case google
    case kakao
    case naver
}
```

이렇게는 알겠는데 각 case의 아이디와 비밀번호를 위한 연관 값??

연관값이 뭘까?? 하고 찾아봤더니

**enum의 연관값은 열거형 내의 하나의 케이스에 대해 각 케이스 인스턴스마다 다른 값들을 가지게 하고 싶을 때 사용한다.** 라고 나와있는 것을 찾았어요

아~ 그럼 google, kakao, naver 각각의 케이스 인스턴스마다 다른 값들을 가지게 해야하는 구나 하고 알게 되었어요.

그럼 어떻게 연관값을 정의하는지 알아볼까요??

```
enum Test {
    case testCaseOne(String, Int)
    case testCaseTwo(String, String)
}
```

Test 라는 enum을 만들었어요 그 안에는 testCaseOne와 testCaseTwo 가 정의되어 있는데, 각 케이스마다 다른 값들을 갖을 수 있도록 각각 다른 타입형들을 넣어 준것을 볼 수 있어요.

이렇게 각기 다른 값들을 갖게 하고 싶으면 연관값을 사용하면 되요

그래서 google, kakao, naver 케이스 각각의 값들을 갖게 해주고 싶으니 연관값을 사용해서 바꾸어 봤어요.

```
enum Site{
    case google(String, String)
    case kakao(String, String)
    case naver(String, String)
}
```

이제 각각의 케이스들은 각기 다른 2개의 String 값들을 받을 수 있게 되었네요!!

그리고 나서 저는 생각을 했어요

이 각기 다른 케이스들을 어떻게 하면 각각 다른 값들에 맞는 출력값을 줄 수 있을까?? 하고 생각했어요

그래서 먼저 간단한 예시를 들어서 이해를 하려고 했죠

```
enum CompassPoint {
    case south
    case north
    case east
    case west
}

let point = CompassPoint.south

switch point {
case CompassPoint.north:
    print(CompassPoint는 north 입니다.)
case CompassPoint.east:
    print(CompassPoint는 east 입니다.)
case CompassPoint.west:
    print(CompassPoint는 west 입니다.)
case CompassPoint.south:
    print(CompassPoint는 south 입니다.)
default:
    print("방향을 찾을 수 없습니다.")
}
```

이런 예시를 들어서 이해를 하려 했어요.

먼저 CompassPoint 라는 enum을 만들고 각각의 케이스에는 south, north, east, west 이 4가지를 정의 했어요

그리고나서 point라는 상수를 만들고 그 상수에는 CompassPoint.south 를 넣어 인스턴스화 하였어요.

그 point 객체는 이제 switch 에서 각각의 케이스를 돌아가며 switch 문에 조건으로 제시된 값과 케이스의 값과 같으면 그 케이스의 실행 구문인 출력문이 출력 될꺼에요.

그래서 point 객체는 CompassPoint.south 이니까 switch 문의 케이스 중 가장 아래의 구문이 실행되겠네요

그럼 이 switch 문을 이용해 google, kakao, naver 각각의 조건에 맞는 출력문을 출력 할 수 있겠다 싶었어요

그럼 똑같이 만들어 보자는 생각에 아래와 같이 만들었어요

```
enum Site {
    case google(String, String)
    case kakao(String, String)
    case naver(String, String)
}

let google = Site.google("kwangjun3952", "1234")

switch google {
case .google(let id, let pw):
    print("구글에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
case .kakao(let id, let pw):
    print("카카오에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
case .naver(let id, let pw):
    print("네이버에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
default:
    print("로그인 실패")
}
```

위와 같은 코드를 만들고 실행하니 `구글에 로그인 하였습니다. - (아이디 - kwangjun3952, 비밀번호 - 1234)`

이렇게 출력문이 실행되었어요.

그럼 각각의 케이스에 서로 다른 값을 넣어 줄 수 있는 연관값과 switch를 이용해 각 케이스에 맞는 값을 출력 할 수 있으니 이것들을 모두 함수로 구현하여 enum안에 넣어주면 되겠다는 생각을 했어요.

그런데 함수를 만드는 과정에서 제가 엄청 고민하고 어려워했던 부분이 바로

switch `self` {} 이 부분이였어요

처음에 저 switch 의 `value` 부분에 **Site**를 넣었더니 아래 케이스에 **Site.goole**를 넣을 수 없었어요

그래서 컴파일러가 self를 넣으라고 조언을 해주었죠.

그래서 **Site.self**를 넣으니 또 오류가 나고 계속 고민을 하다가 그냥 `self`를 넣으니 그때서야 가능했어요

그래서 자세히 살펴보니

![selfImg](https://user-images.githubusercontent.com/42841888/56821282-d5018b80-6888-11e9-9009-8bbbdf91bc9d.png)

이렇게 `self` 는 Site를 뜻하고 있더라구요

`Site` 내에서 `self`는 `Site`라는 것을 그때서야 알게 되었지요.

그래서 아래와 같은 코드를 구현하게 되었습니다.

```
enum Site {
    case google(String, String)
    case kakao(String, String)
    case naver(String, String)

func signIn() {
    switch self {
    case Site.google(let id, let pw):
        print("구글에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
    case Site.kakao(let id, let pw):
        print("카카오에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
    case Site.naver(let id, let pw):
        print("네이버에 로그인 하였습니다. - (아이디 - \(id), 비밀번호 - \(pw)")
    default:
        print("로그인 실패")
        }
    }
}

let google = Site.google("kwangjun3952@gmail.com", "123")
google.signIn()

//구글에 로그인 하였습니다. - (아이디 - kwangjun3952@gmail.com, 비밀번호 - 123)
```
