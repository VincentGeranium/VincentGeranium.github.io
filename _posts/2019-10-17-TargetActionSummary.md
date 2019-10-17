---
layout: post
title:  "Target Action Design Pattern Summary"
date:   2019-10-17
categories: iOS, Swift
---

이 포스트는 edwith iOS 프로그래밍을 공부하고 정리한 글 입니다

[edwith iOS 프로그래밍 - TargetAction](https://www.edwith.org/boostcourse-ios/lecture/16854/)

- - -

### Target Action 디자인 패턴

- Target Action 디자인 패턴은 iOS 환경에서 많이 사용하는 디자인 패턴 중 하나

- Target Action 디자인 패턴에서 객체는 이벤트가 발생할 때 다른 객체에 메시지를 보내는 데 필요한 정보를 포함

- 액션은 특정 이벤트가 발생했을 때 호출할 메서드를 의미한다

    - 타겟은 액션이 호출될 객체를 의미한다
    
- 이벤트 발생시 전송된 메시지를 액션 메시지라고 한다

- 타겟은 프레임워크 객체를 포함한 모든 객체가 될 수 있으나, 보통 컨트롤러가 되는 경우가 일반적이다

- - -

### Target과 Action을 지정하고 디자인 패턴으로 활용하는 이유

- 직접 타겟이 될 객체에 액션에 해당하는 메서드를 호출하면 될 텐데 굳이 Target과 Action을 지정하고 디자인 패턴으로 활용하는 이유

    - 만약 특정 이벤트가 발생했을 때 "abc"라는 이름의 메서드를 호출해야 하는 상황이라고 생각해보자
    
        - 그런데 이 "abc"라는 (액션)메서드는 A라는 클래스에도 정의되어 있고, B라는 클래스에도 정의되어 있는 경우가 있다
        
        - 이렇게 같은 메서드가 여러 클래스에 정의되어 있는 경우도 있고, 그런 클래스의 인스턴스가 여러개인 상황도 있다
        
        - 이런 여러 가지 상황에서 우리가 원하는 객체를 Target으로 저정하면 "abc"라는 액션을 실행할 객체를 상황에 따라서 선택할 수 있다
        
- - -

![targetActionImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/targetActionImage-1.png?raw=true)

![targetActionImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/targetActionImage-2.png?raw=true)

- - -

### Action Method

- 액션 메서드는 특정한 양식이 필요하다 IBAction은 인터페이스 빌더가 메서드를 인지할 수 있도록 해준다

- 스위프트 언어를 활용한 프로그래밍 방식에서는 @objc를 사용하여 메서드를 인지할 수 있도록 한다

    - @objc는 스위프트 클래스를 사용하는 Objective-c 코드가 있거나 Objective-c 유형의 메서드를 사용하는 경우 필요하다
    
```swift

// 프로그래밍 방식
@objc func doSomething(_ sender: Any) {
    // write code
}

// 인터페이스 빌더
@IBAction func doSomething(_ sender: Any) {
    // write code
}

```

- - -

### Control Event

- **컨트롤 이벤트와 액션과의 관계**

    - UIKit에는 "UIButton", "UISwitch", "UIStepper"등 "UIControl"을 상속받은 다양한 컨트롤 클래스가 있다
    
    - 그런 컨트롤 객체에 발생한 다양한 이벤트 종류를 특정 액션 메서드에 연결할 수 있다
    
    - 즉, 컨트롤 객체에서 특정 이벤트가 발생하면, 미리 지정해둔 타켓 액션을 호출하게 된다
    
- - -

### 컨트롤 이벤트의 종류

- **컨트롤 이벤트는 "UIControlEvents"라는 타입으로 정의되어 있다**

- touchDown

    - 컨트롤를 터치했을 떄 발생하는 이벤트
    
    - UIControlEvent.touchDown
    
- touchDownRepeat

    - 컨트롤을 연속 터치 할 때 발생하는 이벤트
    
    - UIControlEvent.touchDownRepeat
    
- touchDragInside

    - 컨트롤 범위 내에서 터치한 영역을 드래그 할 때 발생하는 이벤트
    
    - UIControlEvents.touchDragInside
    
- touchDragOutside

    - 터치 영역이 컨트롤의 바깥쪽에서 드래그 할 때 발생하는 이벤트
    
    - UIControlEvents.touchDragOutside
    
- touchDragEnter

    - 터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔다가 다시 들어왔을 때 발생하는 이벤트
    
    - UIControlEvents.touchDragEnter
    
- touchDragExit

    - 터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔을 때 발생하는 이벤트
    
    - UIControlEvents.touchDragExit
    
- touchUpInside

    - 컨트롤 영역 안쪽에서 터치 후 뗏을때 발생하는 이벤트
    
    - UIControlEvents.touchUpInside
    
- touchUpOutside

    - 컨트롤 영역 안쪽에서 터치 후 컨트롤 밖에서 뗐을때 이벤트
    
    - UIControlEvents.touchUpOutside
    
- touchCancel

    - 터치를 취소하는 이벤트 (touchUp 이벤트가 발생되지 않음)
    
    - UIControlEvents.valueCancel
    
- valueChanged

    - 터치를 드래그 및 다른 방법으로 조작하여 값이 변경되었을 때 이벤트
    
    - UIControlEvents.valueChanged
    
- primaryActionTriggered

    - 버튼이 눌릴때 발생하는 이벤트 (iOS 보다 tvOS에서 사용)
    
    - UIControlEvents.primaryActionTriggered
    
- editingDidBegin

    - "UITextField"에서 편집이 시작될 때 호출되는 이벤트
    
    - UIControlEvents.editingDidBegin
    
- editingChanged

    - "UITextField"에서 값이 바뀔 때마다 호출되는 이벤트
    
    - UIControlEvent.editingChanged
    
- editingDidEnd

    - "UITextField"에서 외부객체와의 상호작용으로 인해 편집이 종료되었을 때 발생하는 이벤트
    
    - UIControlEvents.editingDidEnd
    
- editindDidEndOnExit

    - "UITextField"의 편집상태에서 키보드의 "return" 키를 터치했을 때 발생하는 이벤트
    
    - UIContorlEvents.editingDidEndOnExit
    
- allTouchEvents

    - 모든 터치 이벤트
    
    - UIControlEvents.allTouchEvents
    
- allEditingEvents

    - "UITextField"에서 편집작업의 이벤트
    
    - UIControlEvent.allEditingEvents
    
- applicationReserved

    - 각각의 애플리케이션에서 프로그래머가 임의로 지정할 수 있는 이벤트 값의 범위
    
    - UIControlEvents.applicationReserved
    
- systemReserved

    - 프레임워크 내에서 사용하는 예약된 이벤트 값의 범위
    
    - UIControlEvents.systemReserved
    
- allEvents

    - 시스템 이벤트를 포함한 모든 이벤트
    
    - UIControlEvents.allEvents
