---
layout: post
title:  "MVC 패턴에 대한 간략한 정리"
date:   2019-05-27
categories: iOS, Swift
---

# Study about MVC

---

### 출처

이 포스트는 **Young Kim**님의 포스트를 참고하여 쓴 포스트 임을 미리 밝힙니다

[Young Kim 님의 포스트](https://medium.com/ios-development-with-swift/mvc-%ED%8C%A8%ED%84%B4-in-ios-7751911f8ca8)

---

# MVC (Model - View - Controller)

- iOS 디자인 패턴에는 굉장히 다양한 architectural 패턴들이 존재한다
    - MVC, MVP, MVC-N, MVVM, VIPER 등등
    
- **모든 architectural 패턴들은 "프로그램의 유지보수를 쉽게 그리고 단위 테스트를 할 수 있게"** 라는 **공통된 목표를 가진다**

- 각각의 패턴들은 장단점이 있기에 어떤 패턴이 가장 좋다고 하기는 힘들다

---

# MVC 패턴의 의미

- MVC -> Model-View-Controller의 줄임말

- **Model**은 **데이터에 관한 로직을 담는 부분** , 예를들어 계산기 프로그램을 만든다고 가정하면 값들을 계산하고 저장하는 부분이라고 할 수 있다

- **View**는 **사용자에게 보여지는 화면을 가르킨다** , 예를들어 계산기 프로그램을 만든다고 가정하면 계산된 값들이 보여지는 UI 이다.

- **Controller**는 **Model과 View간의 동작을 관리해준다** , 예를들어 계산기 프로그램을 만든다고 가정하면 사용자가 숫자를 입력 함으로써 View에 변화를 주면, Controller는 View로 입력된 값을 Model로 전달해주는 역활을 한다. 또한 Model에서 값이 계산되면 그 값을 Controller는 View에 전달하여 계산된 값으로 화면을 갱신한다

---

# MVC 패턴의 의미 2

- MVC 패턴을 사용하면 프로그램을 구성하는 코드를 역할에따라 부분적으로 나눌 수 있다

- 예를들어 프로그램의 UI를 바꾸고 싶다면 다른 부분은 그냥 두고 View 부분만 바꿔주면 되고 계산 로직을 바꾸고 싶다면 Model 부분만 바꾸면 된다. 즉, 프로그램이 커져도 유지보수가 상대적으로 쉽다.

---

# MVC 와 iOS

- Apple는 iOS를 개발할 때 MVC를 권장

![mvc](https://user-images.githubusercontent.com/42841888/58394578-eeac1380-807e-11e9-863e-108f28f7a279.png)

- **Model과 View는 절대 서로에게 접근하면 안된다**

- **반면 Controller는 Model과 View에 접근하여 값을 전달하고 받아오는 역활**

- **Controller에서 Model로의 접근, Controller에서 View로의 접근 모두 가능**

---

# Model에서 Controller로의 접근

- 접근은 가능하지만 **MVC 패턴에 어긋남**

- **Model은 데이터의 값을 바꾸고 관리하는것만 해야 한다**

- Model의 값이 바뀌었을 때 Controller에게 값을 **Notification(또는 KVO)** 을 사용하여 해결한다

- **Notification이란** Model의 값이 바뀌었을 때 Model이 Controller에게 바뀐 값을 직접 전달하는것이 아니라 **Model은 자기의 값이 바뀌었다는 사실을 알리면(Notification을 주면), Controller가 이를 듣고 Model에 접근, 이렇게 하면 Model의 바뀐 값에 접근하는 로직을 Controller에 위치 시킬 수 있다**

---

# View에서 Controller로의 접근

- View는 화면을 갱신하는것이 역활, 유저가 View에 값을 입력하거나 터치를 했을때 그 변화를 Controller에 직접 전달하면 안된다

- iOS에서는 이럴때 **Delegate(또는 Data Source)을 사용하여 해결한다**

- **Delegate는** 말 그대로 위임한다는 뜻, **유저가 화면에 값을 입력 할 때 혹은 터치나 드래그를 하여 event를 발생 시켰을 때, 프로그램에서 해야 할 일들을 Controller에게 위임한다, 따라서 View의 변화에 대응하는 로직을 Controller에 위치 시킬 수 있다**
