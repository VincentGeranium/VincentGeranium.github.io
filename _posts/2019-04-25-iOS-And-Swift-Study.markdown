---
layout: post
title:  "AppDelegate를 통한 데이터 전달 구현 과정 중 나만의 정리 - 190425"
date:   2019-04-25
categories: iOS, Swift
---

# iOS-And-Swift-Study

---

### 의도에 따른 코드 작성

각기 다른 뷰 컨트롤러 사이에서 데이터를 주고 받을때

여러가지 방법이 있는데 그 중에서 직접 값을 주고 받을때 자꾸 까먹는 부분이

**값을 화면에 표시하기 위한 아웃렛 변수들**과 **값을 직접 전달 받을 프로퍼티들**을 따로 정의해줘야 하는 것을 까먹는다

**각기 다른 의도를 가지고 있다면 변수들이나 상수들을 따로 따로 만들어줘야 하는다는 점을 기억해야 한다**

```
class ViewController: UIViewController {
    
    @IBOutlet var emailData: UILabel!
    @IBOutlet var updateData: UILabel!
    @IBOutlet var intervalData: UILabel!
    
    var paramEmail: String?
    var paramUpdate: Bool?
    var paramInterval: Double?
}
```

**@IBOutlet var emailData: UILabel!**
**@IBOutlet var updateData: UILabel!**
**@IBOutlet var intervalData: UILabel!**

위의 세가지는 **값을 화면에 표시하기 위한 아웃렛 변수들**

즉, 값을 화면에 표시하기 위한 의도가 있다

**var paramEmail: String?**
**var paramUpdate: Bool?**
**var paramInterval: Double?**

위의 세가지는 **값을 직접 전달받을 프로퍼티들**

즉, 값을 직접 전달받기 위한 의도가 있다

**이렇게 서로 다른 의도가 있으므로 다르게 선언을 해주어야 한다**

---

### 데이터를 전달해 줄 대상 뷰 컨트롤러의 인스턴스를 찾아오는 역활을 하는 코드

각기 다른 뷰 컨트롤러 사이에서 데이터를 주고 받을때

버튼을 누르면 화면 전환과 동시에 데이터가 전달 되는 코드를 작성한다고 가정하자 

(첫번째 화면에서 값을 전달 받고 두번째 화면에서 값을 전달하는 과정을 기억)

(VC1 -> VC2 가 아니라 VC1 <- VC2)

그때, 버튼을 눌렀을 때 동작해야될 구현은 두가지로 나뉜다

첫번째는, 값을 전달

두번째는, 화면의 전환

위에 설명했던 의도가 서로 다르기 때문에 서로 다른 코드를 써줘야 한다

그럼 먼저 값을 전달하는 코드가 쓰였다고 가정하고 **화면의 전환에 대해 코드를 쓰는 과정을 봐보자**

일단 화면을 먼저 전환하려면 그 전환할 객체의 인스턴스가 필요하다

그 인스턴스에 접근하여 그 코드와 화면 전환에 대한 코드를 써주면 된다

먼저 데이터를 전달해 줄 대상 뷰 컨트롤러의 인스턴스를 찾아와야 한다

```
@IBAction func onSubmit(_ sender: Any) {
    
    let PreVC = self.presentingViewController // 나를 띄워주는 객체 // 데이터를 전달해 줄 대상 뷰 컨트롤러의 인스턴스를 찾아오는 코드
    guard let vc = PreVC as? ViewController else { return }
    
    // 값을 전달하는 코드 작성 (나머지 2개 코드 생략)
    vc.paramEmail = self.email.text (이메일 값 전달)
    
    // 이전 화면으로 복귀
    self.presentingViewController?.dismiss(animated: true)

}
```

위의 코드는 버튼을 눌렀을때 화면의 전환과 값의 전달 기능 구현 한 코드이다

그 안에서 내가 가장 헷갈려 했던 **데이터를 전달해 줄 대상 뷰 컨트롤러의 인스턴스를 찾아오는 코드를 봐보자**

```
let PreVC = self.presentingViewController // 나를 띄워주는 객체
    guard let vc = PreVC as? ViewController else { return }
```

**이 코드에서 self.presentingViewController 속성을 통해 이전 뷰 컨트롤러의 인스턴스를 참조할 수 있다**

**vc.paramEmail = self.email.text** 이 인스턴스에 값을 전달해주는 코드

여기서 중요한 점이 있는데 바로 **인스턴스의 타입에 관한 문제이다**

**self.presentingViewController 속성은 UIViewController 타입의 인스턴스를 리턴하므로 ViewController 클래스에 정의되어있는 프로퍼티에 접근 할 수 없다**

**UIViewController 클래스는 ViewController 클래스의 부모이므로, 자식 클래스인 ViewController에 수많은 프로퍼티와 메소드가 추가되엉 있어도 이들에 대한 접근을 할 수 없다**

이러한 문제를 해결하는 방법은 **타입 캐스팅**을 하면 된다

```
guard let vc = PreVC as? ViewController else { return }
```

guard let 을 이용하여 옵셔널 바인딩을 해주고, PreVC as? ViewController 로 타입 캐스팅을 한다

여기서 PreVC 는 self.presentingViewController 이다.

즉, 다시말해 PreVC는 UIViewController 타입이라는 소리이다

---

### 옵셔널 바인딩

어떠한 변수나 상수가 옵셔널 타입으로 정의 되어 있으면

그 옵셔널 값을 전달받거나 혹은 활용할때는 꼭 옵셔널 바인딩 처리를 해주고 사용해야 한다

---

### 앱 델리게이트를 통한 데이터 전달 과정 중 헷갈렸던 점

앱 델리게이트에 변수를 만들고, 값을 전달할 클래스 내부에 앱 델리게이트에 접근 할 수 있도록

앱 델리게이트 인스턴스를 생성 했다

```
@IBOutlet var updateSwitch: UISwitch! // 스위치의 아웃렛 변수 작성

let ad = UIAppliction.shared.delegate as? AppDelegate // 앱 델리게이트 인스턴스 참조 
```

UIAppliction.shared.delegate 구문을 통해 앱 델리게이트의 인스턴스를 가져온 다음

이를 as? AppDelegate, AppDelegate 타입으로 캐스팅한다

그 후에 앱 델리게이트 인스턴스 내부에 있는 프로퍼티에 값을 전달하는 과정 중에서 스위치의 동작 관련 프로퍼티의 리턴 값에 대한 궁굼증이 생겼다

일단 앱 델리게이트 내부에 작성한 프로퍼티는

```
var paramUpdate: Bool?
```

옵셔널 Bool 타입을 정의 했고, 

이 paramUpdate에게 true 또는 false 를 전달하는 코드를 전달 해주는 클래스 내부에서 구현해 주었다

```
ad?.paramUpdate = self.updateSwitch.isOn
```

앱 델리게이트 내부에서 받는 paramUpdate는 옵셔널 Bool 타입이므로 전달 해 줘야 하는 타입도 Bool 타입으로 전달 해주어야 한다

**그 점에서 isOn이 반환하는 값이 true인지 false인지 스위치의 동작을 통해서 결정된다는 것을 알았다**

원래 나의 코드는 

```
ad?.paramUpdate = self.updateSwitch.isOn == true ? true : false
```

이렇게 구현햇는데 어짜피 실제 스위치의 동작에 따라 true, false 값이 반환되므로 굳이 삼항 연산자를 통해 true와 false 값을

전달 할 필요가 없다는 것을 알게 되었다

---

# Github 내의 AppDelegate 를 통한 데이터 전달 구현 전체 코드 링크

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/SubmitValue-Stored)
