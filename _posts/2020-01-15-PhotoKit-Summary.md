---
layout: post
title:  "PhotoKit Summary"
date:   2020-01-15
categories: iOS, Swift
---

이 포스트는 zedd님의 PhotoKit(1),PhotoKit(2)을 공부하고 정리한 내용입니다.

[zedd님의 PhotoKit(1)](https://zeddios.tistory.com/614)

[zedd님의 PhotoKit(2)](https://zeddios.tistory.com/620)

- - -

### PhotoKit

- iOS 및 macOS에서 사진앱의 사진 편집 확장 기능을 지원하는 클래스를 제공

- iOS 및 tvOS에서 사진 앱이 관리하는 사진 및 동영상 asset에 직접 접근 할 수도 있다

- 표시 및 재생을 위해 assets을 가져오고 캐시할 수 있음

- 이미지 및 비디오 내용을 편집하거나, albums, Moments 및 shared albums assets collection을 관리할 수 있다.

- ```모든 PhotoKit객체는 PHObject라는 기본 클래스에서 상속된다```

- - -

### PHObject

- class

- the abstract superclass for Photos model objects (assets and collections).

- ```이 클래스의 인스턴스를 직접 만들거나 사용해서는 안된다```

    - 대신, 구체적인 하위클래스인 `PHAsset, PHAssetCollection, PHCollectionList 및 PHObjectPlaceholder`의 인스턴스로 작업해야한다.
    
- PHObject Class는 localIdentifier 프로퍼티에 따라 isEqual(_:) 및 해시 메소드를 구현한다

    - 이러한 메소드를 사용하여 asset 및 collection 객체를 추적 할 수 있다
    
- - -

### PHAsset

- class

- A representation of an image, video, or Live Photo in the Photos library

- PHAsset은 사용자의 사진 라이브러리에 있는 하나의 asset을 나타내며, 해당 asset의 메타데이터를 제공한다
