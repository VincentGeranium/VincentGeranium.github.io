---
layout: post
title:  "Bar Button Item Summary"
date:   2019-12-27
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Bar Button Item](https://www.edwith.org/boostcourse-ios/lecture/16903/)

- - -

### Bar Button Item

- 바 버튼 아이템은 UIToolbar 또는 UINavigationBar (backBarButtonItem, leftBarButtonItem, rightBarButtonItem등)에 배치할 수 있는 특수한 버튼

- 제목이나 이미지를 보여줄 수 있고 미리 UIBarButtonItem.SystemItem 열거형에 정의된 여러 스타일 중 하나의 스타일로 선택할 수도 있다.

- - -

![BarButtonImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/BarButtonImage-1.png?raw=true)

- TIP : iOS 11에서는 UIBarButtonItem을 오토레이아웃 제약 없이 네비게이션 아이템으로 추가하면 바 버튼 아이템의 프레임이 예상치 못한 크기로 나올 수 있다. 이럴 땐 UIBarButtonItem 객체에 적절한 오토레이아웃 제약을 추가한 후 내비게이션 아이템으로 설정하면 설정한 제약에 따라 알맞은 크기로 볼 수 있다

- - -

#### 주요 프로퍼티

- title : 아이템에 표시되는 제목

```swift
var title: String? { get set }
```

- image : 아이템에 표시되는 이미지

```swift
var image: UIImage? { get set }
```

- style : 아이템의 스타일

```swift
var style: UIBarButtonItem.Style { get set }
```

- width : 아이템 너비 값.

```swift
var width: CGFloat { get set }
```

- tintColor : 아이템에 적용할 색상

```swift
var tintColor: UIColor? { get set }
```

- - -

#### 주요 상수

- UIBarButtonItem.Style : 아이템 스타일 정의.

- UIBarButton.SystemItem : 바 버튼 아이템에 대한 시스템 제공 스타일.

- done : 시스템 완료 버튼

![doneButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/doneButton.png?raw=true)

- add : 더하기 모양 시스템 버튼

![addButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/addButton.png?raw=true)

- edit : 편집 시스템 버튼

![editButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/editButton.png?raw=true)

- cancel : 취소 시스템 버튼

![cancelButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/cancelButton.png?raw=true)

- save : 저장 시스템 버튼

![saveButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/saveButton.png?raw=true)

- reply : 회신 시스템 버튼

![replyButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/replyButton.png?raw=true)

- action : 동작 시스템 버튼

![actionButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/actionButton.png?raw=true)

- trash : 휴지통 시스템 버튼

![trashButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/trashButton.png?raw=true)

- bookmarks : 북마크 시스템 버튼

![bookmarksButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/bookmarksButton.png?raw=true)

- search : 검색 시스템 버튼

![searchButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/searchButton.png?raw=true)

- refresh : 새로고침 시스템 버튼

![refreshButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/refreshButton.png?raw=true)

- stop : 중지 시스템 버튼

![stopButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/stopButton.png?raw=true)

- camera : 카메라 시스템 버튼

![cameraButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/cameraButton.png?raw=true)

- play : 재생 시스템 버튼

![playButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/playButton.png?raw=true)

- pause : 일시 정지 시스템 버튼

![pauseButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/pauseButton.png?raw=true)

- fastForward : 빨리 감기 시스템 버튼

![fastForward](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/fastForward.png?raw=true)

- rewind : 되감기 시스템 버튼

![rewindButton](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/rewindButton.png?raw=true)