---
layout: post
title:  "Image - init"
date:   2019-08-19
categories: Swift, iOS
---

## init

컬렉션 뷰와 커스텀 셀에 대한 공부를 하던 도중에 UIImage를 unwrapping 하는 과정에 대한 궁굼증이 생겨 직접 실험해 보았다

처음 UIImage를 init 하는데, 만약 UIImage에 내가 직접 넣어준 이미지가 없다면 다른 이미지도 대치 해주고 싶었다

그래서 처음 해본 코드는 다음과 같았다

```swift
let koreaImage = UIImage.init(named: "Koreaa") ?? UIImage.init(named: "Error")!
```

위와 같이 하면 Nil-Coalescing Operator ( ?? )를 사용하는 이유가 없어진다.

즉, 잘못된 코드

위의 코드를 playground에서 직접 실행해 보면 다음과 같이 나온다

<img width="1400" alt="imageError" src="https://user-images.githubusercontent.com/42841888/63237195-f7764500-c27b-11e9-807f-7ed8e8ffbf81.png">

Nil-Coalescing Operator를 사용하는 이유는

내 생각에는 nil 값을 돌려주는것보다 안전하게 다른 default 값을 돌려주어

앱을 죽이는 것 보다 살려서 그 오류를 잡아내거나 다른 값으로 대치 하는 느낌이다.

그래서 위의 그림과 같이 코드를 쓰면 실행은 되지만 Nil-Coalescing Operator를 사용하는 이유도

없어지고, 문법에도 맞지 않는다.

그래서 내가 다시 생각한 방법은

```swift
let koreaImage = UIImage.init(named: "Koreaa") ?? UIImage.init()
```

위와 같이 init 메소드를 사용하면 image가 없더라도 앱이 죽지 않고, 아무것도 나타나지 않는다

위의 코드를 playground에서 직접 실행해 보면 다음과 같이 나온다

<img width="1400" alt="imageInit" src="https://user-images.githubusercontent.com/42841888/63238012-5f7a5a80-c27f-11e9-99ef-264ea123f695.png">

그림에서 보이듯이 **w:0 ,h:0**으로 나온다.

즉, 아무런 값이 없다는 뜻이다 그래서 직접 시뮬레이터로 실행해 보면

아무런 이미지가 보이지 않는다

<img width="1400" alt="noImage" src="https://user-images.githubusercontent.com/42841888/63238121-d9aadf00-c27f-11e9-83a5-c4b0e220488d.png">

위의 그림에서 검정색으로 보이는 부분이 내가 직접 지정한 이미지 뷰의 크기와 위치이다

원래라면 아에 아무런 색도 보이지 않고 이미지도 없어야 하는데, 일부러 이미지가 있는지 없는지 확인하기 위해

이미지 뷰의 background를 black로 지정해 놓아서 이미지가 제대로 들어오는지 안들어오는지

확인 할 수 있도록 해놓았다

즉, 지금 위의 그림은 검정색으로 나타났으므로 이미지가 제대로 안들어간 것이라고 보면 된다

이렇게 이미지를 넣고 Nil-Coalescing Operator를 사용하여

앱을 죽이지 않고 이미지가 잘 들어갔는지 확인 혹은 이미지 파일에 대한 오류를 잡아내기 위해

나는 이번 예시를 통해 사용해 보았다

다음에는 Error를 잡는 방법을 따로 공부해서 그 방법으로 Error를 잡는것을 해보려 한다