---
layout: post
title:  "UIActivityViewController Summary"
date:   2020-01-11
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - UIActivityViewController](https://www.edwith.org/boostcourse-ios/lecture/18734/)

- - -

### UIActivityViewController

- 애플리케이션 내에서 특정 아이템을 복사하거나 외부 SNS로 공유하는 내보내기 서비스를 사용하기 위한 것.

- 애플리케이션 내에서 특정 아이템을 복사하거나 외부 SNS로 공유하는 내보내기 서비스는 사용자가 아이템을 다양한 방식으로 활용하도록 도와준다.

- iOS 6 이상부터 사용 가능한 UIActivityViewController 클래스는 아래의 이미지와 같은 내보내기 서비스를 손쉽게 사용할 수 있도록 해준다.

![ActivityVCImage-1]()

- - -


### Activity Item

- UIActivityViewController 클래스를 이용해 아래 아이템을 공유할 수 있다

    - 문자열(String)
    
    - URL 링크(String)
    
    - 이미지(UIImage)
    
    - [UIActivityItemSource 프로토콜을 따르는 커스텀 타입의 인스턴스](https://developer.apple.com/documentation/uikit/uiactivityitemsource)
    
### Activity Type

- UIActivityViewController 클래스가 기본적으로 제공하는 내보내기 서비스의 UIActivity에는 아래와 같은 종류가 있다.

    - 읽기 목록에 추가 ```static let addToReadingList: UIActivityType```
    
    - 에어드롭으로 공유하기 ```static let airDrop: UIActivityType```
    
    - 연락처에 지정 ```static let assignToContact: UIActivityType```
    
    - Paste Board에 복사 ```static let copyToPasteboard: UIActivityType```
    
    - 메일 보내기 ```static let mail: UIActivityType```
    
    - 메시지 보내기 ```static let message: UIActivityType```
    
    - iBooks에서 열기 ```static let openInIBooks: UIActivityType```
    
    - 페이스북에 공유하기 ```static let postToFacebook: UIActivityType```
    
    - Flickr에 공유하기 ```static let postToFlickr: UIActivityType```
    
    - Tencent Weibo에 공유하기 ```static let postToTencentWeibo: UIActivityType```
    
    - 트위터에 공유하기 ```static let postToTwitter: UIActivityType```
    
    - Vimeo에 공유하기 ```static let postToVimeo: UIActivityType```
    
    - SinaWeibo에 공유하기 ```static let postToWeibo: UIActivityType```
    
    - 프린트 ```static let print: UIActivityType```
    
    - 카메라 롤에 저장하기 ```static let saveToCameraRoll: UIActivityType```
    
    - PDF 생성(iOS 11부터 사용가능) ```static let markupAsPDF: UIActivityType```
    
- - -

### UIActivityViewController의 메서드 및 프로퍼티

```swift
init(activityItems: [Any], applicationActivities: [UIActivity]?)
```
- 초기화 메소드로, UIActivityViewController 객체를 반환한다

    - activityItems: [Any] 공유하려는 아이템으로 UIActivitySource 프로토콜을 준수하는 객체를 배열 형태로 넣어 줄 수 있다.

    - applicationActivities: [UIActivity]? 애플리케이션이 지원하는 커스텀 서비스를 나타내는 UIActivity 객체의 배열로, nil 값이 될 수 있다.

```swift
var completionWithItemsHandler: UIActivityViewControllerCompletionWithItemsHandler?
```

- 컨트롤러를 닫은 후 실행할 완료 핸들러이다.

```swift
var excludedActivityTypes: [UIActivityType]?
```

- UIActivityType 중 사용하지 않을 서비스를 지정한다.

- - -

### 샘플 코드

```swift

// 1. UIActivityViewController 초기화, 공유 아이템 지정
let imageToShare: UIImage = UIImage(named: "image.png")
let urlToShare: String = "https://vincentgeranium.github.io"
let textToShare: String = "Hi, I'm Vincent"

let activityViewController = UIActivityViewController(activityItems: [imageToShare, urlToShare, textToShare], applicationActivities: nil)

// 2. 기본적으로 제공되는 서비스 중 사용하지 않을 UIActivityType 제거(선택사항)
activityViewController.excludedActivityTypes = [UIActivityType.addToReadingList, UIActivityType.assignToContact]

// 3. 컨트롤러를 닫은 후 실행할 완료 핸들러 지정
activityViewController.completionWithItemsHandler = { (activity, success, item, error) in
    if success {
    // 성공시 작업
    } else {
    // 실패시 작업
    }
}

//4. 컨트롤러 나타내기(iPad에서는 팝 오버로, iPhone과 iPod에서는 모달로 나타낸다)
self.present(activityViewController, animated: true, completion: nil)
```