---
layout: post
title:  "Photos Framework Summary"
date:   2019-12-05
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Photos Framework](https://www.edwith.org/boostcourse-ios/lecture/16867/)

- - -

### What is Photos Framework

- Photos 프레임워크는 iOS 및 macOS 에서 사진 애플리케이션, 사진 확장 기능을 지원하는 클래스를 제공한다

- Photos 프레임워크를 통해 iOS 및 tvOS에서 iCloud 사진 라이브러리를 포함하여 사진 및 비디오에 직접 접근할 수 있다

- Photos 프레임워크를 사용하여 화면에 표시 및 재생할 에셋을 검색하고 이미지 또는 비디오를 편집하거나 앨범, 틀별한 순간 및 iCloud 공유 앨범과 같은 에셋을 사용하여 작업할 수 있다

- - -

### Photos Framework의 특징 및 개념

- Photos Framework에는 iOS 및 tvOS에서 사용자의 사진 라이브러리와 직접 작업하기 위한 여러 가지 기능이 있다

### Asset

![AssetImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AssetImg.png?raw=true)

- - -

### Asset Collection

![AssetCollectionImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AssetCollectionImg.png?raw=true)

- - -

### Collection List

![CollectionList](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CollectionList.png?raw=true)

- - -

### 객체 가져오기 및 변경요청

- Photos Framework 모델 클래스 (PHAsset, PHAssetColletion, PHCollectionList)의 인스턴스는 사진 애플리케이션에서 Asset(이미지, 비디오, 라이브 포토), Asset Collection(앨범, 특별한 순간) 및 사용자가 작업하는 항목을 나타낸다.

    - Collection List(앨범 폴더, 특별한 순간) 이 객체는 읽기 전용이며 변경할 수 없다. 그리고 메타 데이터만 포함한다.

- 해당 객체를 사용하여 작업해야 하는 데이터를 가져와서 에셋 및 컬랙션 작업을 할 수 잇다

    - 변경 요청을 하려면 변경 요청 객체를 만들고 이를 공유 PHPhotosLibrary 객체에 명시적으로 알려준다

    - 이 아키텍처를 사용하면 다수의 스레드 혹은 다수의 애플리케이션과 동일한 에셋을 사용하여 쉽고 안전하며 효율적으로 작업할 수 있다.

- - -

### 변경을 관찰

- 가져온 에셋 및 컬렉션에 대한 변경 핸들러를 등록하려면 공유 PHPhotoLibrary 객체를 사용해야한다

    - 다른 애플리케이션이나 기기가 에셋의 콘텐츠나 메타 데이터 또는 컬렉션의 리스트를 변경할 때마다 애플리케이션에 알려준다
    
- PHChange 객체는 변경 전후의 객체 상태에 대한 정보를 제공하여 쉽게 컬렉션뷰 또는 유사한 인터페이스를 업데이트 할 수 있다

- - -

### Photos 애플리케이션의 기능들을 지원.

- PHCollectionList 클래스를 사용해 사진 애플리케이션의 특별한 순간 계층에 해당하는 에셋을 찾는다

    - 버스트, 파노라마 사진 및 고프레임 비디오를 식별하려면 PHAsset 클래스를 사용
    
- iCloud 사진 라이브러리가 활성화되면 Photos Framework의 에셋과 컬렉션에는 동일한 iCloud 계정의 사용할 수 있는 내용이 반영된다

- - -

### 에셋과 미리보기 로딩 및 캐싱

- PHImageManager 클래스를 사용해 지정된 크기로 에셋의 이미지를 요청하거나 비디오 에셋에 사용할 AVFoundation 객체를 요청한다

- - -

### 에셋 콘텐츠 편집

- PHAsset 및 PHAssetChangeRequest 클래스는 편집을 위해 사진 또는 비디오를 요청하여 사진 라이브러리에 편집한 내용을 반영하는 메서드를 정의한다

- - -

### Photos 라이브러리 상호작용

- PHPhotoLibrary 객체를 사용하여 사진 콘텐츠에 접근하고, 에셋 및 컬렉션을 변경할 수 있도록 애플리케이션의 사용자 권한을 얻는다. 권한을 얻으면 사진 라이브러리가 변경될 때 변경사항을 전달받을 수도 있다

    - `PHPhotoLibrary : 사용자의 사진 라이브러리에 대한 접근 및 변경을 관리하는 공유 객체`
    
- - -

### 에셋 검색과 조사

- 이 모델 클래스는 사진 라이브러리의 콘텐츠(에셋, 컬렉션)을 나타낸다

- 읽기 전용이며 변경이 불가능하고 메타 데이터만 포함한다
    
- 에셋과 컬렉션을 사용하려면 이 클래스를 사용하여 지정한 쿼리와 일치하는 객체를 가져온다

    - `PHAsset` -> 사진 라이브러리의 이미지, 비디오, 라이브 포토를 나타낸다

    - `PHAssetCollection` -> 특별한 순간, 사용자정의 앨범 또는 스마트 앨범과 같은 사진, 에셋 그룹을 나타낸다

    - `PHCollectionList` -> 특별한 순간, 사용자정의 앨범, 특별한 순간들 연도와 같은 에셋 컬렉션이 포함된 그룹을 나타낸다

    - `PHCollection` -> 에셋 컬렉션 및 컬렉션 리스트의 추상 수퍼 클래스

    - `PHObject` -> 모델 객체(에셋 및 컬렉션)의 추상 수퍼 클래스

    - `PHFetchResult` -> 가져오기 메서드에서 반환된 에셋 또는 컬렉션의 정렬된 목록

    - `PHFetchOptions` -> 에셋 또는 컬렉션 객체를 가져올 때 Photos에서 반환하는 결과에 필터링, 정렬 등 영향을 주는 옵션

- - -

### 에셋 콘텐츠 로딩

- 이 클래스를 사용하여 이미지, 비디오, 라이브 포토 콘텐츠를 요청할 수 있다

    - `PHImageManager` -> 미리보기 썸네일 및 에셋과 전체 크기의 이미지 또는 비디오 데이터를 검색하거나 생성하는 방법을 제공한다
    
    - `PHCachingImageManager` -> 많은 에셋을 일괄적으로 미리 로딩하기 위해 최적화된 에셋과 관련된 썸네일 및 전체 크기의 이미지 또는 비디오 데이터를 검색하거나 생성하는 방법을 제공한다
    
    - `PHImageRequestOptions` -> 이미지 매니저로부터 요청한 에셋 이미지의 영향을 주는 옵션들
    
    - `PHVideoRequestOptions` -> 이미지 매니저로부터 요청한 비디오 에셋 데이터의 영향을 주는 옵션들
    
    - `PHLivePhotoRequestOptions` -> 이미지 매니저로부터 요청한 라이브 포토 에셋의 영향을 주는 옵션들
    
    - `PHLivePhoto` -> 캡쳐 직전과 직후 순간의 움직임 및 소리가 포함된 라이브 사진을 표현한다
    
- - -

### 변경 요청

- 에셋이나 컬렉션을 변경하려면 변경 요청 객체를 만들고 명시적으로 사진 라이브러리에 반영한다

- 이 방법을 사용하면 여러 스레드 또는 여러 애플리케이션 및 애플리케이션 확장에서 같은 에셋을 가지며 쉽고, 안전하며 효율적으로 작업할 수 있다

    - `PHAssetChangeRequest` -> 사진 라이브러리 변경 블록(클로저)에서 사용하기 위해 에셋의 생성, 삭제, 메타 데이터 수정할 변경 요청 객체이다
    
    - `PHAssetCollectionChangeRequest` -> 사진 라이브러리 변경 블록(클로저)에서 사용하기 위해 에셋 컬렉션을 생성, 삭제, 수정할 변경 요청 객체이다
    
    - `PHCollectionChangeRequest` -> 사진 라이브러리 변경 블록(클로저)에서 사용하기 위해 컬렉션 리스트 생성, 삭제, 수정할 변경 요청 객체이다
    
- - -

### 에셋 콘텐츠 수정

- 애플리케이션 또는 확장 프로그램에서 이 클래스들을 사용하여 사진 라이브러리의 편집 및 반영을 위해 에셋 데이터에 접근한다

- 사진들은 각 수정 사항을 버전별로 에셋 및 보정 데이터를 관리하므로 애플리케이션 또는 확장 프로그램을 사용하여 다른 기기에서도 이전에 수정한 내용을 되돌리거나 계속 사용할 수 있다

- 사진 편집 확장 기능을 만들려면 이 클래스들과 PhotosUI 프레임워크와 같이 사용

    - `PHContentEditingInput` -> 편집할 에셋의 이미지, 비디오, 라이브 포토의 콘텐츠에 대한 정보와 접근 권한을 제공하는 컨테이너이다
    
    - `PHContentEditingOutput` -> 에셋의 사진, 비디오, 라이브 포토의 콘텐츠를 편집한 결과를 제공하는 컨테이너이다
    
    - `PHAdjustmentData` -> 편집 효과를 재구성하거나 되돌릴 수 있는 에셋의 사진, 비디오, 라이브 포토 콘텐츠의 수정사항에 대한 설명이다

    ![AdjustmentDataImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AdjustmentDataImg.png?raw=true)

    - `PHContentEditingInputRequestOptions` -> 에셋의 콘텐츠를 수정하도록 요청할 때 이미지, 비디오 데이터 전송에 영향을 주는 옵션
    
    - `PHLivePhotoEditingContext` -> 라이브 포토의 사진, 비디오, 오디오 콘텐츠를 수정하기 위한 편집 세션이다
    
    - `PHLivePhotoFrame` -> 편집 컨텍스트에서 라이브 포토의 단일 프레임에 대한 이미지 콘텐츠를 제공하는 컨테이너이다
    
- - -

### 변경사항 관찰

- Photo Framework는 다른 애플리케이션이나 다른 기기에서 사진의 정보를 변경할 때마다 애플리케이션에 알려준다

- 이러한 객체는 변경 전후의 객체 상태에 대한 정보를 제공하므로 사용자 인터페이스를 쉽게 업데이트하여 일치시킬 수 있다

    - `PHPhotoLibraryChangeObserver` -> 사진 라이브러리에서 발생한 변경사항을 위해 구현할 수 있는 프로토콜
    
    - `PHChange` -> 사진 라이브러리에서 발생한 변경사항에 대한 설명이다
    
    - `PHObjcetChangeDetails` -> 에셋 또는 컬렉션 객체에서 발생한 변경사항에 대한 설명이다
    
    - `PHFetchResultChangeDetails` -> 가져오기 결과에 나열된 에셋 또는 컬렉션에서 발생한 변경사항에 대한 설명이다
    
- - -

### 에셋 리소스로 작업하기

- 에셋 리소스 객체는 각 에셋의 데이터 저장소를 나타낸다. 이러한 객체를 사용해 에셋을 직접 백업하고 복원할 수 있다

    - `PHAssetResource` -> 사진 라이브러리의 사진, 비디오 라이브 포토 에셋과 관련된 기본 데이터 리소스이다
    
    - `PHAssetCreationRequest` -> 사진 라이브러리 변경 블록(클로저)에서 사용하기 위해 기본 데이터 리소스에서 새로운 에셋을 생성하라는 요청
    
    - `PHAssetResourceCreationOptions` -> 기본 리소스에서 새로운 에셋을 만드는데 영향을 주는 옵션들이다
    
    - `PHAssetResourceManager` -> 에셋과 관련된 리소스에 대한 기본 데이터 저장소에 접근하는 방법을 제공
    
    - `PHAssetResourceRequestOptions` -> 에셋 리소스 관리자가 요청한 기본 에셋 데이터 전달에 영향을 주는 옵션이다