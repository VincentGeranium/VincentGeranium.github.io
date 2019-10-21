---
layout: post
title:  "Gesture Recognizer Summary"
date:   2019-10-18
categories: iOS, Swift
---

이 포스트는 edwith의 부스트코스 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Gesture Recognizer](https://www.edwith.org/boostcourse-ios/lecture/17992/)

- - -

### Gesture Recognizer

- 제스처 인식기는 여러 제스처 관련 이벤트를 인식할 수 있다

- 특정 제스처 이벤트가 일어날 때 마다 각 타깃에 맞는 액션 메시지를 보내어 제스처 관련 이벤트를 처리할 수 있다

- - -

### UIGestureRecognizer Class

- UIGestureRecognizer 클래스는 특정 제스처 인식기에 대한 동작을 정의한다

- 또한 델리게이트 객체를 활용하여 일부 동작을 더욱 세밀하게 사용자화 할 수 있다

- - -

### UIGestureRecognizer의 하위 클래스

- 아래의 7가지 UIGestureRecognizer 하위 클래스를 통해 여러 제스처를 인식할 수 있다

    - 1) UITapGestureRecognizer
        
        - 싱글탭 또는 멀티탭 제스쳐
        
    - 2) UIPinchGestureRecognizer
    
        - 핀치(Pinch) 제스처
        
    - 3) UIRotationGestureRecognizer
    
        - 회전 제스쳐
        
    - 4) UISwipeGestureRecognizer
    
        - 스와이프(swipe) 제스쳐
        
    - 5) UIPanGestureRecognizer
    
        - 드래그(Drag) 제스쳐
        
    - 6) UIScreenEdgePanGestureRecognizer
    
        - 화면 가장자리 드래그 제스쳐
        
    - 7) UILongPressGestureRecognizer
    
        - 롱프레스(long-press) 제스쳐
        
- 제스쳐 인식기를 사용하기 위해서 타깃-액션 연결을 설정한 후 UIView의 메서드인 addGestureRecognizer(_:) 메서드를 통해 뷰에 연결한다

    - 제스쳐가 인식되면 해당 제스쳐 인벤트에 연결된 타깃에 액션 메시지가 전달된다
    
    - 호출되는 메서드는 아래의 메서드 구현 형식 중 하나와 같아야 한다
    
```swift

@IBAction func myActionMethod()
@IBAction func myActionMethod(_ sender: UIGestureRecognizer)

```

- 윈도우는 뷰에 터치 이벤트를 전달하기 전에 뷰에 추가된 제스쳐 인식기에 터치 이벤트를 전달한다

- 제스쳐 인식기가 터치 이벤트를 인식했을 경우 뷰는 터치 이벤트를 받지 못하고, 제스쳐 인식기가 터치 이벤트를 인식하지 못했을 경우 터치 이벤트를 뷰가 받게 된다

- 일반적인 제스처 인식기의 동작의 흐름은 cancelsTouchesInView, delaysTouchesBegan, delaysTouchedEnded 프로퍼티의 값에 영향을 받는다

- - -

### UIGestureRecognizer의 주요 메서드

- init(target: Any?, action: Selector?)

    - 제스처 인식기를 타깃-액션의 연결을 통해 초기화 한다.

- func location(in: UIView?) -> CGPoint

    - 제스처가 발생한 좌표를 반환한다.
    
- func addTarget(Any, action: Selector)

    - 제스처 인식기 객체에 타깃과 액션을 추가한다.
    
- func removeTarget(Any?, action: Selector?)

    - 제스처 인식기 객체로부터 타깃과 액션을 제거한다.
    
- func require(toFail: UIGestureRecognizer)
    
    - 여러 개의 제스처 인식기를 가지고 있을 때, 제스처 인식기 사이의 의존성을 설정한다.
    
- - -

### UIGestureRecognizer의 주요 프로퍼티

- var state: UIGestureRecognizerState

    - 현재 제스처 인식기의 상태를 나타낸다
    
- var view: UIView?

    - 제스처 인식기가 연결된 뷰 이다
    
- var isEnabled: Bool

    - 제스처 인식기가 사용 가능한 상태인지를 나타낸다
    
- var cancelsTouchInView

    - 제스처가 인식되었을 때 터치 이벤트가 뷰로 전달되는 여부에 영향을 미친다
    
        - 이 프로퍼티가 true(기본값)이고 제스처 인식기가 제스처를 인식했다면, 해당 제스처의 터치는 뷰로 전달되지 않는다
        
        - 이전에 전달된 터치들은 touchesCancelled(_:with:) 메시지를 통해 취소된다
        
        - 제스처 인식기가 제스처를 인식 못하거나 이 프로퍼티의 값이 false라면 뷰가 모든 터치를 전달받게 된다
        
- var delayTouchesBegan

    - began 단계에서 제스터 인식기가 추가된 뷰에 터치의 전달 지연 여부를 결정한다
    
- var delayTouchesEnded

    - end 단계에서 제스처 인식기가 추가된 뷰에 터치의 전달 지연 여부를 결정한다
    
- - -

### 제스처 인식기 추가해보기

- 인터페이스 빌더를 사용해 제스터 인식기 추가 , 코드작성을 통해 제스처 인식기 추가

[프로젝트 파일 repo](https://github.com/VincentGeranium/Swift-Study/tree/master/gestureRecognizerExampleProject)

- - -

### iOS의 Standard Gesture

- 1) Tap : 컨트롤을 활성화하거나 항목을 선택한다

- 2) Drag : 아이템을 좌우 또는 화면으로 드래그 할 수 있다

- 3) Flick : 빠르게 스크롤하거나 화면을 넘길 수 있다

- 4) Swipe : 이전 화면으로 돌아가거나 테이블 뷰에서 숨겨진 삭제 버튼을 표시할 수 있다

- 5) Double tap : 이미지 또는 콘텐츠를 확대하거나 다시 축소한다

- 6) Pinch : 이미지를 세밀하게 확대하거나 다시 축소할 수 있다

- 7) Touch and Hold : 편집 가능한 텍스트 또는 선택 가능한 텍스트에서 수행돌 경우 커서 지정을 위한 확대보기각 표시된다. 컬렉션 뷰의 경우 항목을 재배치할 수 있는 모드로 진입한다.

- 8) Shake: 실행 취소 또는 실행 얼럿을 띄운다

- 9) Rotate : 이미지 또는 뷰를 돌린다.

- - -

### Apple Documentation

[UIGestureRecognizer - UIKit / Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uigesturerecognizer)

[Human Interface Guidelines - Gesture](https://developer.apple.com/design/human-interface-guidelines/ios/user-interaction/gestures/)