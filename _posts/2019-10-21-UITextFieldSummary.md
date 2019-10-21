---
layout: post
title:  "UITextField Summary"
date:   2019-10-21
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Gesture Recognizer의 사용 부분](https://www.edwith.org/boostcourse-ios/lecture/17993/)

- - -

### UITextField

- 텍스트 필드는 사용자 인터페이스에서 편집 가능한 텍스트 영역을 나타낸다

- 사용자가 키보드를 통해 입력하는 문자열 데이터를 활용할 수 있다

- 텍스트 필드는 Target-Action 디자인  패턴과 델리게이트 객체를 사용하여 텍스트 편집 이벤트에 관해 다룬다

- - -

### 키보드 보여주기 / 숨기기

- 사용자가 텍스트 필드를 탭 하게 되면 텍스트 필드는 자동으로 first responder가 되면서 시스템은 키보드를 보여준다

- 사용자가 키보드를 사용하여 입력을 하게되면 텍스트 필드에 텍스트가 입력된다

- 텍스트 필드를 자동으로 탭하는 방법 외에도 becomeFirstResponder() 메서드를 직접 호출해서 키보드를 나타나게 할 수 있다

- 키보드를 숨기기 위해 resignFirstResponder() 또는 endEditing(_:) 메서드를 호출할 수 있다

- - -

### 인터페이스 빌더에서 설정 가능한 속성

[Apple Documentation - UITextField](https://developer.apple.com/documentation/uikit/uitextfield#1653000)

- 텍스트 필드의 속성은 Apple Documentation - UITextField 링크의 Table 1을 참조

- 키보드 속성은 Apple Documentation - UITextField 링크의 Table 2를 참조

- - -

### 텍스트 필드 델리게이트

- 텍스트 필드는 델리게이트 객체의 도움을 받아 텍스트 편집의 이벤트 등을 관리한다

- 사용자가 텍스트 필드를 통한 작업을 할 때 이와 관련된 이벤트들을 델리게이트 객체에게 알리고 이를 사용하여 여러 이벤트를 처리할 수 있다

- 텍스트 필드의 델리게이트 객체의 메서드에 관한 자세한 정보는 UITextFieldDelegate를 참조

[Apple Documentation - UITextFieldDelegate](https://developer.apple.com/documentation/uikit/uitextfielddelegate)

- - -

### UITextField 클래스의 주요 프로퍼티

- var delegate: UITextFieldDelegate?

    - 텍스트 필드의 델리게이트 객체
    
- var text: String?

    - 텍스트 필드에 보여지는 문자열
    
- var placeholder: String?

    - 텍스트 필드에 아무것도 입력되어 있지 않을 때 기본으로 보이게 되는 문자열. 텍스트 필드에 텍스트를 입력하게 되면 사라진다
    
- var font: UIFont?
    
    - 텍스트의 폰트를 설정
    
- var textColor: UIColor?
    
    - 텍스트의 색상을 설정한다
    
- var textAligment: NSTextAligment

    - 텍스트의 정렬을 설정한다
    
- var isEditing: Bool

    - 현재 텍스트 필드가 편집 모드에 있는지 나타낸다
    
- var background: UIImage?

    - 텍스트 필드가 enable 되어 있을 때의 배경 이미지를 나타낸다
    
- var disabledBackground: UIImage?

    - 텍스트 필드가 disabled 되어 있을 때의 배경 이미지를 나타낸다
    
- var clearButtonMode: UITextFieldViewMode

    - 텍스트 필드의 텍스트를 모두 지울 수 있는 컨트롤을 텍스트 필드에 나타나게 할 수 있다
    
- - -

### UITextFieldDelegate 프로토콜의 주요 메서드

- func textFieldShouldBeginEditing(UITextField)
    
    - 델리게이트 객체에게 텍스트 필드에서 텍스트 편집 시작을 요청한다
    
- func textFieldDidBeginEditing(UITextField)

    - 델리게이트에게 텍스트 필드에서 텍스트 편집이 시작되었음을 델리게이트 객체에게 알린다
    
- func textField(UITextField, shouldChangeCharactersIn: NSRange, replacementString: String)

    - 델리게이트 객체에게 현재 텍스트의 수정을 요청한다
    
- func textFieldShouldEndEditing(UITextField)

    - 델리게이트 객체에게 텍스트 편집 중지를 요청한다
    
- - -

[Apple Documentation - Article (Using Responders and the Responder Chain to Handle Events)](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events)