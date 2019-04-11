---
layout: post
title:  "Alert Controller Code Review"
date:   2019-04-11
categories: Swift
---

# Code Review

---

## 코드[Github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-04-10-AlertController-Study)

---

- 뷰 안에 어떠한 것을 표현하고 싶으면 먼저 code로 구현시 class viewController 안에 정의 해 주어야 한다
- 앱의 생명주기(시점)에 따라 구현해야 할 내용이 다르면 그 시점에 알맞는 메소드 안에 구현해야 한다
    - example
    
    ```
    override func viewDidLoad() {
        super.viewDidLoad()
        enterButton.setTitle("Enter, for: .normal)
    }
    ```

- 뷰의 로드가 끝나는 시점에 enterButton의 타이틀과 상태를 정해주는 메소드를 구현했다.
    - 이렇게 시점에 맞는 구현을 해줘야 할 경우 앱 라이프 사이클에 맞는 메소드에 코드를 구현해야 한다
- .frame 는 어떤 객체의 frame 위치와 사이즈를 정해준다
    - frame = CGRect()는 구조체인데 frame의 위치와 크기를 지정해 줄 수 있다
- Summary: The frame rectangle, which describes the view’s location and size in its superview’s coordinate system
- .titleLabel 은 UILabel의 프로퍼티이다
    - 뷰에 나타나는 버튼의 currentTitle 속성 값을 표시하는 것이다
    - 더 나아가 버튼 title의 여러 속성에 접근하여 수정히거나 정해줄 수 있다
- .addTarget은 대상 객체와 액션(동작) 매소드를 컨트롤과 연결한다고 나와 있다
    - Summary :Associates a target object and action method with the control.
    - 즉 addTarget 의 정의를 보면 
    
    ```
    func addTarget(_ target: Any?, action: Selector, for controlEvents: UIControl.Event)
    ```
    
    - 이렇게 나와있는데 taget으로 지정하면 그 객체와 action에 지정된 액션 메소드를 for controlEvents로 지정한 컨트롤과 연결이 되는 것이다
    - 예를들어
    
    ```
    enterButton.addTarget(self, action: #selector(enterButtonAction(_:)), for: .touchUpInside)
    ```
    
    - self라고 했으니 enterButton 자기 자신과 action으로 지정된 #selector로 지정한 따로 정의한 enterButtonAction(_:)라는 메소드를 .touchUpInside라는 컨트롤과 연결되는 것이다
- .textAligment = 로 하여 = 뒤에 원하는 글자의 위치 배열을 지정해 줄 수 있다
    - 예를들어
    
    ```
    textLabel.textAlignment = .center
    ```
    
    - textLabel의 text의 위치를 중간으로 맞춰주겠다는 것이다
- @objc func는 어떤 객체의 메소드를 정의할때 꼭 @objc와 함께 사용하여 정의해야 한다
- UIAlertAction()는 사용자가 alert 버튼을 눌렀을때 수행할 수 있는 작업을 명시해주거나 정의해준다
- .addAction은 어떠한 동작을 선언한 UIAlertAction()의 객체를 alert 또는 action sheet에 첨부하는 것이다
    - 예를들어 alertControllerAction.addAction(up) 이라면
        - UIAlertAction()의 객체인 up을 alert 또는 action sheet 내의 창에 첨부한다는 것이다
        - alertControllerAction 이 코드상에서 UIAlertController로 정의되어 있어서 위의 예시 코드는 alert에 첨부되는 것이다
- present()메소드는 present내에 명시된 뷰 컨트롤러를 모달로 표시한다
    - present() 메소드는 viewDidAppear(_:) 다음에 호출된다
