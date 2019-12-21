---
layout: post
title:  "Scroll View Summary"
date:   2019-12-21
categories: iOS, Swift
---

### What is Scroll View ?

- 스크롤 뷰는 스크롤 뷰 안에 포함된 뷰를 상, 하, 좌, 우로 스크롤 할 수 있고 확대 및 축소가 가능한 뷰

#### 스크롤 뷰를 상속 받아 활용되는 뷰

- UITableView, UICollectionView, UITextView등 여러 UIKit 클래스가 있다.

![ScrollViewImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ScrollViewImage.png?raw=true)

- - -

### 스크롤뷰 상호작용

#### 주요 프로퍼티

- delegate : 스크롤뷰 객체의 델리게이트

```swift
weak var delegate: UIScrollViewDelegate? { get set }
```

- UIScrollViewDelegate 프로토콜에 의해 선언된 메소드 델리게이트가 UIScrollView 클래스의 메세지에 응답

- - -

### 콘텐츠 크기 및 오프셋 관리

#### 주요 프로퍼티

- contentSize : 콘텐츠뷰의 크기

```swift
var contentSize: CGSize { get set }
```

- contentOffset : 콘텐츠뷰의 원점이 스크롤뷰의 원점에서 오프셋 된 지점

```swift
var contentOffset: CGPoint { get set }
```

#### 주요 메서드

- setContentOffset(_:animated:) : 스크롤뷰의 원점에 대한 콘텐츠뷰의 오프셋 설정

```swift
func setContentOffset(_ contentOffset: CGPoint, animated: Bool)
```

- - -

### 콘텐츠 삽입 동작 관리

#### 주요 프로퍼티

- contentInset : 콘텐츠뷰와 안전 영역 또는 스크롤뷰 가장자리에 간격

```swift
var contentInset: UIEdgeInsets { get set }
```

- - -

### 스크롤뷰 구성

#### 주요 프로퍼티

- isScrollEnabled : 스크롤링이 사용 가능한지 아닌지를 결정하는 Bool 값

```swift
var isScrollEnabled: Bool { get set }
```

- isDirectionallLockEnabled : 스크롤이 특정 방향으로 고정할지를 결정하는 Bool 값

```swift
var isDirectionalLockEnabled: Bool { get set }
```

- isPagingEnabled : 스크롤뷰에서 페이징을 사용할 수 있는 여부를 결정하는 Bool 값

```swift
var isPagingEnabled: Bool { get set }
```

- scrollsToTop : 스크롤 할 수 있는 제스처를 사용할지를 결정하는 Bool 값

```swift
var scrollsToTop: Bool { get set }
```

- bounces : 스크롤뷰가 가장자리를 통과해서 다시 튀어나오는지 제어하는 Bool 값

```swift
var bounce: Bool { get set }
```

- alwaysBounceVertical : 세로 스크롤이 콘텐츠뷰의 끝에 도달할 때 튀어 오르기가 항상 발생하는지 결정하는 Bool 값

```swift
var alwaysBounceVertical: Bool { get set }
```

- alwaysBounceHorizontal : 가로 스크롤이 콘텐츠뷰의 끝에 도달할 때 튀어 오르기가 항상 발생하는지 결정하는 Bool 값

```swift
var alwaysBounceHorizontal: Bool { get set }
```

- - -

### 스크롤링 상태 가져오기

#### 주요 프로퍼티

- isTracking : 사용자가 스크롤을 시작하기 위해 콘텐츠를 터치한 여부를 반환

```
var isTracking: Bool { get }
```

- isDragging : 사용자가 콘텐츠를 스크롤할고 있는지 나타내는 Bool 값

```swift
var isDragging: Bool { get }
```

- isDecelerating : 사용자가 손가락을 떼었을 때 콘텐츠가 스크롤뷰에서 움직이지 않고 있는지를 반환

```swift
var isDecelerating: Bool { get }
```

- decelerationRate: 사용자가 손가락을 뗀 후의 감속도를 결정하는 부동 소수점 값

```swift
var decelerationRate: CGFloat { get set }
```

- - -

### 스크롤 인디케이터 및 새로고침 제어 관리

#### 주요 프로퍼티

- indicatorStyle : 스크롤 인디케이터의 스타일

```swift
var indicatorStyle: UIScrollViewIndicatorStyel { get set }
```

- showHorizontalScrollIndicator : 가로 스크롤 바 표시 여부를 제어하는 Bool 값

```swift
var showHorizontalScrollIndicator: Bool { get set }
```

- showVerticalScrollIndicator : 세로 스크롤 바 표시 여부를 제어하는 Bool 값

```swift
var showVerticalScrollIndicator: Bool { get set }
```

- - -

### 특정 위치로 스크롤 하기

#### 주요 메서드

- scrollRectToVisible(_:animated:) : 콘텐츠의 특정 위치로 스크롤 하여 화면에 표시

```swift
func scrollRectToVisible(_ rect: CGRect, animated: Bool)
```

- - -

### 확대 및 축소

#### 주요 프로퍼티

- panGestureRecognizer : 팬 제스처를 제어하기 위한 제스처 인스턴스

```swift
var panGestureRecognizer: UIPanGestureRecognizer { get }
```

- pinchGestureRecognizer : 핀치 제스처를 제어하기 위한 제스처 인스턴스

```swift
var pinchGestureRecognizer: UIPinchGestureRecognizer? { get }
```
- zoomScale : 스크롤뷰 콘텐츠에 적용되는 현재 비율

```swift
var zoomScale: CGFloat { get set }
```
- maximumZoomScale : 스크롤뷰 콘텐츠에 적용되는 최대 배율

```swift
var maximumZoomScale: CGFloat { get set }
```

- minimumZoomScale : 스크롤뷰 콘텐츠에 적용되는 최소 배율

```swift
var minimumZoomScale: CGFloat { get set }
```

- isZoomBouncing : 확대 및 축소가 지정한 배율 제한을 초과했음을 나타내는 Bool 값

```swift
var isZoomBouncing: Bool { get }
```

- isZooming : 콘텐츠 뷰가 현재 확대 또는 축소되어 있는지를 나타내는 Bool 값

```swift
var isZooming: Bool { get }
```

- bouncesZoom : 크기 조정이 최대 또는 최소 제한을 초과할 때 튀어 오르는 애니메이션을 보여줄지 결정하는 Bool 값

```swift
var bouncesZoom: Bool { get set }
```

####  주요 메서드

- zoom(to:animated:) : 콘텐츠 특정 영역 확대

```swift
func zoom(to rect: CGRect, animated: Bool)
```

- setZoomScale(_:animated:) : 현재 배율을 지정

```swift
func setZoomScale(_ scale: CGFloat, animated: Bool)
```

- - - 

### 키보드 관리

#### 주요 프로퍼티

- keyboardDismissMode : 스크롤뷰에서 드래그가 시작될 때 키보드가 해제되는 방식

```swift
var keyboardDismissMode: UIScrollViewKeyboardDismissMode { get set }
```

- - -

### UIScrollViewDelegate Protocol

#### 스크롤 및 드래그

- scrollViewDidScroll(_:) : 콘텐츠뷰를 스크롤 할 때 델리게이트에 알림

```swift
optional func scrollViewDidScroll(_scrollView: UIScrollView)
```

- scrollViewWillBeginDragging(_:) : 스크롤뷰에서 콘텐츠 스크롤을 시작할 시점을 델리게이트에 알림

```swift
optional func scrollViewWillBrginDragging(_ scrollView: UIScrollView)
```

- scrollViewWillEndDragging(_:withVelocity:targetContentOffset:) : 스크롤뷰의 드래그가 끝나기 직전에 델리게이트에 알림

```swift
optional func scrollViewWillEndDragging(_ scrollView: UIScrollView, withVelocity velocity: CGPoint, targetContentOffset: UnsafeMutablePointer<CGPoint>)
```

- scrollViewDidEndDragging(_:willDecelerate:) : 스크롤뷰의 드래그가 끝났을 때 델리게이트에 알림

```swift
optional func scrollViewDidEndDragging(_ scrollView: UIScrollView, willDecelerate decelerate: Bool)
```

- scrollViewShouldScrollToTop(_:) : 스크롤뷰가 콘텐츠의 맨 위로 스크롤 해야 하는 경우 델리게이트에 동작 여부를 물어봄

```swift
options func scrollViewShouldScrollToTop(_ scrollView: UIScrollView)
```

- scrollViewWillBeginDecelerating(_:) : 스크롤링 동작이 감속되기 시작하고 있다고 델리게이트에 알림

```swift
optional func scrollViewWillBeginDecelerating(_ scrollView: UIScrollView)
```

- scrollViewDidEndDecelerating(_:) : 스크롤링 동작 감속이 끝났을 때 델리게이트에 알림

```swift
optional func scrollViewDidEndDecelerating(_ scrollView: UIScrollView)
```

#### 확대 및 축소

- viewForZooming(in:) : 스크롤뷰에서 확대 및 축소를 할 때 확대 및 축소를 할 뷰 인스턴스를 요청

```swift
optional func viewForZooming(in scrollview: UIScrollView) -> UIView?
```

- scrollViewWillBeginZooming(_:with:) : 스크롤뷰의 콘텐츠 확대가 시작될 때 델리게이트에 알림

```swift
optional func scrollViewWillBeginZooming(_ scrollView: UIScrollView, with view: UIView?)
```

- scrollViewDidEndZooming(_:with:atScale:) : 스크롤뷰의 콘텐츠 확대가 완료될 때 델리게이트에 알림

```swift
optional func scrollViewDidEndZooming(_ scrollView: UIScrollView, with view: UIViwe?, atScale scale: CGFloat)
```

- scrollViewDidZoom(_:) : 스크롤뷰의 확대 및 축소 배율이 변경될 떄 델리게이트에 알림

```swift
optional func scrollViewDidZoom(_ scrollView: UIScrollView)
```

#### 스크롤 애니메이션

- scrollViewDidEndScrollingAnimation(_:) : 스크롤뷰의 스크롤 애니메이션이 끝날 때 델리게이트에 알림

```swift
optional func scrollViewDidEndScrollingAnimation(_ scrollView: UIScrollView)
```
