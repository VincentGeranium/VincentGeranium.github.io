---
layout: post
title:  "What is DataSource and Delegate ?"
date:   2020-01-05
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - DataSource와 Delegate?](https://www.edwith.org/boostcourse-ios/lecture/16908/)

- - -

### 컬렉션뷰 데이터소스와 델리게이트

![dataSourceAndDelegateImage]()

#### 데이터소스

- 컬렉션뷰 데이터소스 객체는 컬렉션뷰와 관련하여 가장 중요한 객체이며, 필수로 제공해야한다.

- 컬렉션뷰의 콘텐츠(데이터)를 관리하고 해당 콘텐츠를 표현하는 데 필요한 뷰를 만든다.

- 데이터소스 객체를 구현하려면 UICollectionViewDataSource 프로토콜을 준수하는 객체를 만들어야 한다.

- 데이터소스 객체는 최소한 collectionView(_:numberOfItemsInSection:)과 collectionView(_:cellForItemAt:) 메서드를 구현해야하며 나머지 메서드는 선택사항이다

#### 필수 메서드

- collectionView(_:numberOfItemsInSection:)
    
    - 지정된 섹션에 표시할 항목의 개수를 묻는 메서드.
    
```swift
func collectionView(_collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int
```

- collectionView(_:cellForItemAt:)

    - 컬렉션뷰의 지정된 위치에 표시할 셀을 요청하는 메서드.
    
```swift
func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell
```

#### 주요 선택 메서드

- numberOfSections(in:)
    
    - 컬렉션뷰의 섹션의 개수를 묻는 메서드.
    
    - 이 메서드를 구현하지 않으면 섹션 개수 기본 값은 1.
    
```swift
optional func numberOfSections(in collectionView: UICollectionView) -> Int
```
- collectionView(_:canMoveItemAt:)

    - 지정된 위치의 항목을 컬렉션뷰의 다른 위치로 이동할 수 있는지를 묻는 메서드.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, canMoveItemAt indexPath: IndexPath) -> Bool
```

- collectionView(_:moveItemAt:to:)

    - 지정된 위치의 항목을 다른 위치로 이동하도록 지시하는 메서드.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, moveItemAt sourceIndexPath: IndexPath, to destinationIndexPath: IndexPath)
```
- - -

#### 델리게이트

- 컬렉션뷰 델리게이트 프로토콜은 컬렉션뷰에서 셀의 선택 및 강조표시를 관리하고 해당 셀에 대한 작업을 수행할 수 있는 메서드를 정의한다.

- 이 프로토콜의 메서드는 모두 선택사항이다.

#### 주요 메서드

- collectionView(_:shouldSelectItemAt:)

    - 지정된 셀이 사용자에 의해 선택될 수 있는지 묻는 메서드.
    
    - 선택이 가능한 경우 true로 응답하며 아닌 경우는 false로 응답.

```swift
optional func collectionView(_ collectionView: UICollectionView, shouldSelectItemAt indexPath: IndexPath) -> Bool
```

- collectionView(_:didSelectItemAt:)

    - 지정된 셀이 선택되었음을 알리는 메서드.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, didSelectionItemAt indexPath: IndexPath)
```

- collectionView(_:shouldDeselectItemAt:)

    - 지정된 셀의 선택이 해제될 수 있는지 묻는 메서드.
    
    - 선택 해제가 가능한 경우 true로 응답, 그렇지 않으면 false로 응답.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, shouldDeselectItemAt indexPath: IndexPath) -> Bool
```

- collectionView(_:didDeselectItemAt:)
    
    - 지정된 셀의 선택이 해제되었음을 알리는 메서드.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, didDeselectItemAt indexPath: IndexPath)
```

- collectionView(_:shouldHighlightItemAt:)

    - 지정된 셀이 강조될 수 있는지 묻는 메서드.
    
    - 강조해야 하는 경우 true로 응답, 그렇지 않다면 false로 응답.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, shouldHighlightItemAt indexPath: IndexPath) -> Bool
```

- collectionView(_:didHighlightItemAt:)

    - 지정된 셀이 강조되었을 때 알려주는 메서드.
    
```swift
optional func collectionView(_ collectionView: UICollectionView, didHighlightItemAt indexPath: IndexPath)
```

- collectionView(_:didUnhighlightItemAt:)

    - 지정된 셀이 강조가 해제될 때 알려주는 메서드
    
```swift
optional func collectionView(_ collectionView: UICollectionView, didUnhighlightItemAt indexPath: IndexPath)
```