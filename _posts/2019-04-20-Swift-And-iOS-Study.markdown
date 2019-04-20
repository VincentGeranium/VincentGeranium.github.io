---
layout: post
title:  "뷰 컨트롤러 간 데이터 전송 코드 구현 중 알게된 점 정리"
date:   2019-04-20
categories: iOS, Swift
---

# 190420-Swift-And-iOS-Study

## 전체 코드 

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/transferValue)

---

타입선언은 
- "상수 또는 변수 키워드" + "상수 또는 변수의 이름" + "타입"
    - 예시
    
    ```
    let someName: Int = 10
    var someNumber: String = "Su-a"
    ```
    
- 처음 상수 또는 변수를 만들고 그에 맞는 타입을 선언한 뒤 초기값을 넣어주지 않을 경우 초기화(initialize)가 필요하다

클래스 변수 또는 상수에 넣어 인스턴스 만들기
- "상수 또는 변수 키워드" + "이름" + "=" + "인스턴스 화 시킬 클래스 이름" + "()"
    - 예시
    
    ```
    class someClass () {
        var loverName = "Jun"
    }
    
    let sua = someClass()
    ```

---

### 이미 시스템 상에 정해져 있는 스위치의 위치만을 정해주기

스위치를 코드로만 화면상에 보이게 하고 싶었다

그래서 UISwitch를 인스턴스화 하여

```
let autoRenewalSwitch = UISwitch()
```

위의 상수에 넣어 주었다

그리고 나서 문제가 스위치는 이미 시스템 상에서 default되어 있는 width값과 height값이 있는데 frame을 써서 어떻게 위치를 잡는지 몰랐다

그래서 Definition을 들어가 보니

```
extension UIView {

    open var frame: CGRect

    open var bounds: CGRect

    open var center: CGPoint

    open var transform: CGAffineTransform

    @available(iOS 4.0, *)
    open var contentScaleFactor: CGFloat

    open var isMultipleTouchEnabled: Bool

    open var isExclusiveTouch: Bool

    open func hitTest(_ point: CGPoint, with event: UIEvent?) -> UIView?

    open func point(inside point: CGPoint, with event: UIEvent?) -> Bool

    open func convert(_ point: CGPoint, to view: UIView?) -> CGPoint

    open func convert(_ point: CGPoint, from view: UIView?) -> CGPoint

    open func convert(_ rect: CGRect, to view: UIView?) -> CGRect

    open func convert(_ rect: CGRect, from view: UIView?) -> CGRect

    open var autoresizesSubviews: Bool

    open var autoresizingMask: UIView.AutoresizingMask

    open func sizeThatFits(_ size: CGSize) -> CGSize

    open func sizeToFit()
}
```

UIView를 확장한 것 안에 프로퍼티로 frame가 있었다,

frame은 CGRect 타입이였고 그래서 CGRect를 들어가보니

```
public struct CGRect {

    public var origin: CGPoint

    public var size: CGSize

    public init()

    public init(origin: CGPoint, size: CGSize)
}
```

CGRect는 구조체로 되어있었으며, 그 안에 origin이라는 프로퍼티가 있었다 그 프로퍼티는 CGPoint 타입으로 받아서

한번 더 CGPoint를 알아봐야겠다는 생각에 CGPoint를 들어가 봤다

```
public struct CGPoint {

    
    public var x: CGFloat

    public var y: CGFloat

    public init()

    public init(x: CGFloat, y: CGFloat)
}
```

그랫더니 내가 찾던 width와 height값이 이미 정해져있고 x와 y값만 정해줄 수 있는게 나왔다 그래서 스위치의 x와 y값만 지정해서 위치를 찾아주는 코드를 쓸 수 있게 되었다,

아래가 바로 그 코드이다.

```
autoRenewalSwitch.frame.origin = CGPoint(x: 345, y: 336)
```

---

### TextField

이메일을 입력받는 TextField를 만들고 싶었다

그래서 먼저 이 TextField의 frame을 잡고, view.addSubview() 를 통해서 textfield를 화면에 띄우게 했다

```
emailTextField.frame = CGRect(x: 94,
                              y: 234,
                              width: 300,
                              height: 30)
view.addSubview(emailTextField)
```

그런데 이게 왠걸?? 화면에는 아무것도 보이지 않았다, 그래서 생각을 해보니 textfield의 틀을 잡아주어야겠다는 생각을 했다

내가 생각한 틀을 잡아주겠다는 것은 틀에 스타일을 잡아야겠다는 것이였다

그래서 스타일을 보니 여러가지 스타일들이 있었다

```
emailTextField.borderStyle = .bezel
emailTextField.borderStyle = .line
emailTextField.borderStyle = .none
emailTextField.borderStyle = .roundedRect
```

이 4가지의 스타일을 다 하나씩 해봐가면서 각각의 스타일을 비교해봤다, 그랬더니 none를 빼고는 다 화면에 보일 수 있도록 스타일이 되어있었다

그러고 나서 한가지 더 구현해주고 싶은게 생각이 났는데 textfield 안에 반투명하게 이 textfield 안에 어떤 값을 넣어 주어야 하는지에 대한 설명을

보여주고 싶었다.

그래서 코드를 하나씩 뒤져가며 찾아보니

```
emailTextField.placeholder = "이메일을 입력해 주세요"
```

위와 같이 .placeholder를 쓰고 문자열을 넣어주면 저 문자열이 그대로 나왔다

---

### Button

나는 두개의 뷰 컨트롤러를 만들어 하나의 뷰 컨트롤러에서 다른 뷰 컨트롤러로 데이터를 전송하는 것을 구현하고 싶었다

그래서 버튼을 만들어 버튼을 누르면 데이터가 전송되도록 하려고 버튼을 만들었다

그래서 일단 버튼의 타이틀을 만들어 주려고 했는데, 버튼만의 키워드를 사용하여 타이틀을 만들어 줘야 했다

.setTitle 바로 이 키워드이다

```
submitButton.setTitle("Submit", for: .normal)
```

이 setTitle은 두개의 인자값을 받는데 처음에 들어가는 인자값은 타이틀의 이름

두번째에 들어가야 할 인자값은 이 버튼 타이틀의 상태를 받는다

내가 두번째의 인자값이 어떤것이 들어가는지 궁굼해서 더 알아봤더니 두번째 인자값에는

UIControl.state가 들어가야 했다

UIControl은 일단 무엇인지 궁굼해서 definition으로 들어갔다

아래와 같이 나와 있었다

```
open class UIControl : UIView {

    
    open var isEnabled: Bool // default is YES. if NO, ignores touch events and subclasses may draw differently

    open var isSelected: Bool // default is NO may be used by some subclasses or by application

    open var isHighlighted: Bool // default is NO. this gets set/cleared automatically when touch enters/exits during tracking and cleared on up

    open var contentVerticalAlignment: UIControl.ContentVerticalAlignment // how to position content vertically inside control. default is center

    open var contentHorizontalAlignment: UIControl.ContentHorizontalAlignment // how to position content horizontally inside control. default is center

    open var effectiveContentHorizontalAlignment: UIControl.ContentHorizontalAlignment { get } // how to position content horizontally inside control, guaranteed to return 'left' or 'right' for any 'leading' or 'trailing'

    
    open var state: UIControl.State { get } // could be more than one state (e.g. disabled|selected). synthesized from other flags.

    open var isTracking: Bool { get }

    open var isTouchInside: Bool { get } // valid during tracking only

    
    open func beginTracking(_ touch: UITouch, with event: UIEvent?) -> Bool

    open func continueTracking(_ touch: UITouch, with event: UIEvent?) -> Bool

    open func endTracking(_ touch: UITouch?, with event: UIEvent?) // touch is sometimes nil if cancelTracking calls through to this.

    open func cancelTracking(with event: UIEvent?) // event may be nil if cancelled for non-event reasons, e.g. removed from window

    
    // add target/action for particular event. you can call this multiple times and you can specify multiple target/actions for a particular event.
    // passing in nil as the target goes up the responder chain. The action may optionally include the sender and the event in that order
    // the action cannot be NULL. Note that the target is not retained.
    open func addTarget(_ target: Any?, action: Selector, for controlEvents: UIControl.Event)

    
    // remove the target/action for a set of events. pass in NULL for the action to remove all actions for that target
    open func removeTarget(_ target: Any?, action: Selector?, for controlEvents: UIControl.Event)

    
    // get info about target & actions. this makes it possible to enumerate all target/actions by checking for each event kind
    
    open var allTargets: Set<AnyHashable> { get }

    open var allControlEvents: UIControl.Event { get } // list of all events that have at least one action

    
    // set may include NSNull to indicate at least one nil target
    // list of all events that have at least one action
    
    open func actions(forTarget target: Any?, forControlEvent controlEvent: UIControl.Event) -> [String]? // single event. returns NSArray of NSString selector names. returns nil if none

    
    // send the action. the first method is called for the event and is a point at which you can observe or override behavior. it is called repeately by the second.
    open func sendAction(_ action: Selector, to target: Any?, for event: UIEvent?)

    open func sendActions(for controlEvents: UIControl.Event) // send all actions associated with events
}
```

UIControl은 UIView를 상속받고 있었고 그 안에 state가 있는데 그 state는 UIControl.State를 타입으로 받고 잇었다

그럼 State가 뭔지 알아봐야 해서 한번 더 들어가봤더니

```
 public struct State : OptionSet {

        public init(rawValue: UInt)

        
        public static var normal: UIControl.State { get }

        public static var highlighted: UIControl.State { get } // used when UIControl isHighlighted is set

        public static var disabled: UIControl.State { get }

        public static var selected: UIControl.State { get } // flag usable by app (see below)

        @available(iOS 9.0, *)
        public static var focused: UIControl.State { get } // Applicable only when the screen supports focus

        public static var application: UIControl.State { get } // additional flags available for application use

        public static var reserved: UIControl.State { get } // flags reserved for internal framework use
    }
}
```

State는 위와 같이 구조체였고 OptionSet protocol을 받고 있었다

OptionSet protocol은 나중에 알아보고, 일단 State 구조체 안에보면 여러 프로퍼티가 있었는데 그 각각의 프로퍼티가 의미하는 바가 달랐고

자신이 원하는 버튼 타이틀의 상태를 지정해 줄 수 있다

또한 setTitleColor 키워드를 사용하여 title의 색상을 지정해 줄 수 있다

그리고 버튼의 프레임을 짜고 화면에 올린뒤 눌러보면 아무런 액션을 하지 않는다

왜그런가 했더니 Action에 대해 아무런 코드나 명령이 없어서 화면 내에서 눌리는 모습도 안보여지고 그냥 text만 있는듯한 느낌이었다

그럴땐 따로 addTarget 키워드를 사용하여 어디서, 어떤 액션을, 어떤 이벤트 형태로 이 세가지 인자값을 받아 버튼을 활성화 할 수 있게 했다

```
submitButton.addTarget(self, action: #selector(didTabSubmitButton), for: .touchUpInside)
```

여기서 한가지 더 궁굼한점이 뭐냐하면 action: 이 인자값인데 여기에 #selector 키워드를 구현하여아 한다 그 #selector 안에는
어떠한 액션을 할 것인지에 대해 함수를 만들어 놓은것을 넣어 주어야 하는데 위의 코드에서 보이는 didTabSubmitButton는 아래와 같다

```
@objc func didTabSubmitButton() {
        self.present(secondVC, animated: true)   
    }
```

위의 함수는 다음 뷰 컨트롤러로 가는 액션 함수이다.

즉, 버튼을 누르면 다음 뷰 컨트롤러로 갈 수 있게 된다

---

### Stepper

스테퍼는 +와 - 버튼이 같이 있는 모양으로 생겼다 그래서 이 스테퍼가 어떻게 구현 되어있을까 하고 궁굼해서 definition으로 가봤다 그랬더니 다음과 같이 나오는데

```
@available(iOS 5.0, *)
open class UIStepper : UIControl {

    
    open var isContinuous: Bool // if YES, value change events are sent any time the value changes during interaction. default = YES

    open var autorepeat: Bool // if YES, press & hold repeatedly alters value. default = YES

    open var wraps: Bool // if YES, value wraps from min <-> max. default = NO

    
    open var value: Double // default is 0. sends UIControlEventValueChanged. clamped to min/max

    open var minimumValue: Double // default 0. must be less than maximumValue

    open var maximumValue: Double // default 100. must be greater than minimumValue

    open var stepValue: Double // default 1. must be greater than 0

    
    // The tintColor is inherited through the superview hierarchy. See UIView for more information.
    @available(iOS 6.0, *)
    open var tintColor: UIColor!

    
    // a background image which will be 3-way stretched over the whole of the control. Each half of the stepper will paint the image appropriate for its state
    @available(iOS 6.0, *)
    open func setBackgroundImage(_ image: UIImage?, for state: UIControl.State)

    @available(iOS 6.0, *)
    open func backgroundImage(for state: UIControl.State) -> UIImage?

    
    // an image which will be painted in between the two stepper segments. The image is selected depending both segments' state
    @available(iOS 6.0, *)
    open func setDividerImage(_ image: UIImage?, forLeftSegmentState leftState: UIControl.State, rightSegmentState rightState: UIControl.State)

    @available(iOS 6.0, *)
    open func dividerImage(forLeftSegmentState state: UIControl.State, rightSegmentState state: UIControl.State) -> UIImage?

    
    // the glyph image for the plus/increase button
    @available(iOS 6.0, *)
    open func setIncrementImage(_ image: UIImage?, for state: UIControl.State)

    @available(iOS 6.0, *)
    open func incrementImage(for state: UIControl.State) -> UIImage?

    
    // the glyph image for the minus/decrease button
    @available(iOS 6.0, *)
    open func setDecrementImage(_ image: UIImage?, for state: UIControl.State)

    @available(iOS 6.0, *)
    open func decrementImage(for state: UIControl.State) -> UIImage?
}
```

정말 수 많은 파라미터들이 있는데 내가 지금 만드는 스테퍼는 +버튼을 누르면 1씩 증가하고 -를 누르면 1씩 감소하여 레이블에 보여주게 만들고 싶었다

그래서 어떤 프로퍼티를 사용해야 할까 하고 봤더니

```
open var value: Double // default is 0. sends UIControlEventValueChanged. clamped to min/max
```

이것을 사용하면 될것 같앗다 스테퍼의 value를 이용하여 +를 누르면 1씩 증가 -를 누르면 1씩 감소하게 그래서 아래와 같은 코드를 구현하여 스테퍼에 addTarget을 해주었다

```
@objc func didTabRenewalCycleStepper() {
        let value = Int(subRenewalCycleStepper.value)
        self.subRenewalCycleLabel.text = "\(value)분 마다 갱신"
       
```

그리고 한가지 더 만약에 1씩이 아니고 5씩 혹은 다른 숫자만큼 +를 누르면 증가 -를 누르면 감소하게 하고 싶으면,

스테퍼의 

```
open var stepValue: Double // default 1. must be greater than 0
```

를 바꿔주면 된다, 나도 궁굼해서 한번 5로 바꿔봤더니 +를 누르면 5씩 증가하였고 -을 누르니 5씩 감소하였다

그리고 max값과 min값을 지정해 줄 수도 있는데 그것은 아래의 프로퍼티를 이용하여 지정해주어야 한다

```
open var minimumValue: Double // default 0. must be less than maximumValue

open var maximumValue: Double // default 100. must be greater than minimumValue
```
