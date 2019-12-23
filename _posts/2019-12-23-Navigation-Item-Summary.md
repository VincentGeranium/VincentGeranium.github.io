---
layout: post
title:  "Navigation Item Summary"
date:   2019-12-23
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Navigation Item](https://www.edwith.org/boostcourse-ios/lecture/16903/)

- - -

### Navigation Item

- 내비게이션 바의 콘텐츠를 표시하는 객체이다.

- 뷰 컨트롤러가 전환될 때마다 내비게이션 바는 하나의 공동 객체이지만, 내비게이션 아이템은 각각의 뷰 콘트롤러가 가지고 있는 프로퍼티이다.

    - 즉, 내비게이션 바가 내비게이션 컨트롤러와 연관이 있다면 내비게이션 아이템은 해당 뷰 컨트롤러와 연관이 있다는 말
    
- 보통 내비게이션 바에서 보여지는 중앙 타이틀, 좌측 바 버튼, 우측 바 버튼 등이 내비게이션 아이템의 프로퍼티이다

![navigationItemImage-1]()

- - -

#### Navigation Item의 주요 프로퍼티

- title : 내비게이션 바에 표시되는 내비게이션 아이템의 제목, 기본값은 nil.

```swift
var title: String? { get set }
```

- backBarButtonItem : 내비게이션 바에서 뒤로 버튼이 필요할 때 사용할 바 버튼 항목.

```swift
var backBarButtonItem: UIBarButtonItem? { get set }
```

- hidesBackButton : 뒤로 버튼이 숨겨져 있는지를 결정하는 Bool 값

```swift
var hidesBackButton: Bool { get set }
```

- - -

#### Navigation Item의 주요 메서드

- setHidesBackButton(_:animated:) : 뒤로 버튼이 숨겨져 있는지를 설정하고, 전환 애니메이션 효과 적용

```swift
func setHideBackButton(_ hidesBackButton: Bool, animated: Bool)
```

- - -

### Navigation Item Customizing

- 내비게이션 아이템은 크게 좌, 우 바 버튼 아이템과 중앙 타이틀 영역이 있다.

- 좌측 바 버튼, 우측 바 버튼 아이템의 경우 타입은 UIBarButtonItem이다.

- 상황에 따라서 커스텀 뷰를 넣어서 구현할 수 있다.

#### 프로퍼티

- titleView : 중앙 타이틀 영역의 뷰

```swift
var titleView: UIView? { get set }

// TIP : 중앙 타이틀 영역에 뷰를 상속받은 (UILabel, UIView, UIImageView등등) 클래스들을 표현할 수 있다
```

- leftBarButtonItems : 좌측 아이템 영역의 UIBarButtonItem의 바 버튼 아이템 배열

```swift
var leftBarButtonItems: [UIBarButtonItem]? { get set }
```

- leftBarButtonItem : 좌측 아이템 영역의 UIBarButtonItem 중에 가장 좌측 바 버튼 아이템

```swift
var leftBarButtonItem: UIBarButtonItem? { get set }
```

- rightBarButtonItems : 우측 아이템 영역의 UIBarButtonItem의 바 버튼 아이템 배열

```swift
var rightBarButtonItem: [UIBarButtonItem]? { get set }
```

- rightBarButtonItem : 우측 아이템 영역의 UIBarButtonItem 중에 가장 우측 바 버튼 아이템

```swift
var rightBarButtonItem: UIButtonItem? { get set }
```

#### 메서드

- setLeftBarButtonItems(_:animated:) : 좌측 아이템 영역에 UIBarButtonItem 타입의 객체들을 순차적으로 설정하고 애니메이션 효과를 적용

```swift
func setLeftBarButtonItems(_Items: [UIBarButtonItem]?, animated: Bool)
```

- setLeftBarButton(_:animated:) : 좌측 아이템 영역에  UIBarButtonItem 타입의 객체를 설정하고 애니메이션 효과를  적용

```swift
func setLeftBarButton(_ item: UIBarButtonItem?, animated: Bool)
```

- setRightBarButtonItems(_animated:) : 우측 내비게이션 아이템 영역에 UIBarButtonItem 타입의 객체들을 순차적으로 설정하고 애니메이션 효과를 적용

```swift
func setRightBarButtonItems(_items: [UIBarButtonItem]?, animated: Bool)
```

- setRightBarButton(_:animated:) : 우측 아이템 영역에 UIBarButtonItem 타입의 객체를 설정하고 애니메이션 효과를 적용

```swift
func setRightBarButton(_ item: UIBarButtonItem?, animated: Bool)
```