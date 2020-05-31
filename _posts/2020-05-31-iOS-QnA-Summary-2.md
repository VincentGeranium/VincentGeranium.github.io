---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 10 (bound와 frame의 차이점, Foundation Kit, User Interface를 구성하는데 필수적인 프레임워크는?, Cocoa Touch Framework)"
date:   2020-05-31
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [edwith - UIKit](https://www.edwith.org/boostcourse-ios/lecture/17995/)

- [edwith - Cocoa touch](https://www.edwith.org/boostcourse-ios/lecture/17994/)

- [Apple Docs - UIKit](https://developer.apple.com/documentation/uikit)

- - -
- - -

### bound와 frame의 차이점

- bound와 frame 모두 해당 주체의 너비, 높이와 위치 좌표 값(x,y)를 나타낸다.

    - **frame은 부모 뷰의 좌표시스템에서 자신의 위치를 나타낸다.**
    
        - **frame의 x,y 좌표를 변경하게 되면 자기 자신의 위치가 변경된다.**
    
    - **bound는 자신의 내부 좌표 시스템을 사용하여 위치를 나타낸다.**
    
        - **bound의 x,y 좌표를 변경하면 자신이 포함하는 하위 뷰들의 위치가 옮겨지게 된다.**

### Cocoa Touch Framework?

<img width="1058" alt="CocoaTouchFrameworkImg-1" src="" title="CocoaTouchFrameworkImg-1$">

- **코코아 터치 프레임워크는 iOS 애플리케이션 개발 환경이다.**

    - **코코아 터치 프레임워크는 애플리케이션의 다양한 기능 구현에 필요한 여러 프레임워크를 포함하는 최상위 레벨의 프레임워크이다.**
    
        - `코코아`라는 단어는 Objective-C 런타임을 기반으로하고, NSObject를 상속받는 모든 클래스 또는 객체를 가리킬 때 사용한다.
        
        - `코코아` 또는 `코코아 터치`는 iOS 또는 macOS의 전반적인 기능을 활용해 애플리케이션을 제작할 때 사용하는 프레임워크이다.
        
        - **코코아 터치는 핵심 프레임워크인 UIKit과 Foundation을 포함한다.**

- 참고로 코코아 프레임워크는 macOS 애플리케이션 제작에 사용하는 프레임워크이다.

     - 즉, 코코아 터치 프레임워크와는 다른것.
        
### Foundation Kit은 무엇이고 어떤 클래스들이 포함되어있는지.

<img width="1058" alt="FoundationDocsImg-1" src="" title="FoundationDocsImg-1">

- Foundation Kit은 Cocoa Touch framework에 포함되어 있는 프레임워크 중 하나이다.

    - **String, Int 등의 원시 데이터 타입과 컬렉션 타입 및 운영체제 서비스를 사용해 앱의 기본적인 기능을 관리하는 프레임워크이다.**
    
    - **Foundation 프레임워크는 데이터 저장 및 지속성, 텍스트 처리, 날짜 및 시간 계산, 정렬 및 필터링 그리고 네트워킹을 포함하여 앱 및 프레임워크에 대한 기본 계층 기능을 제공한다. Foundation에서 정의한 클래스, 프로토콜 및 데이터 유형은 macOS, iOS, watchOS 및 tvOS SDK에서 사용된다.**
    
### iOS 앱을 만들고 User Interface를 구성하는데 필수적인 프레임워크는?

- **UIKit 이다.**

<img width="1058" alt="UIKitDocsImg-1" src="" title="UIKitDocsImg-1">

- UIKit 소개

    - **UIKit은 iOS 애플리케이션의 사용자 인터페이스를 구현하고 이벤트를 관리하는 프레임워크이다.**
    
        - UIKit 프레임워크는 제스처 처리, 애니메이션, 그림 그리기, 이미지 처리, 텍스트 처리 등 사용자 이벤트 처리를 위한 클래스를 포함한다.
        
        - 테이블뷰, 슬라이더, 버튼, 텍스트 필드, 얼럿 창 등 애플리케이션의 화면을 구성하는 요소를 포함한다.
        
        - UIKit 클래스 중 UIResponder에서 파생된 클래스나 사용자 인터페이스에 관련된 클래스는 애플리케이션의 메인 스레드(혹은 메인 디스패치 큐)에서만 사용 해야한다.
        
        - UIKit은 iOS와 tvOS 플랫폼에서 사용한다.
        
- UIKit 기능별 요소

    - 사용자 인터페이스
    
        - View and Control : 화면에 콘텐츠 표시
        
        - View Controller : 사용자 인터페이스 관리
        
        - Animation and Haptics : 애니매이션과 햅틱을 통한 피드백 제공
        
        - Window and Screen ; 뷰 계층을 위한 윈도우 제공
        
    - 사용자 액션
    
        - Touch, Press, Gesture : 제스처 인식기를 통한 이벤트 처리 로직
        
        - Drag and Drop : 화면 위에서 드래그 앤 드롭 기능
        
        - Peek and Pop : 3D 터치에 대응한 미리 보기 기능
        
        - Keyboard and Menu : 키보드 입력을 처리 및 사용자 정의 메뉴 표시

    