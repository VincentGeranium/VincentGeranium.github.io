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

- `모든 PhotoKit객체는 PHObject라는 기본 클래스에서 상속된다`

- - -

### PHObject

- class

    - the abstract superclass for Photos model objects (assets and collections).

- `이 클래스의 인스턴스를 직접 만들거나 사용해서는 안된다`

    - 대신, 구체적인 하위클래스인 `PHAsset, PHAssetCollection, PHCollectionList 및 PHObjectPlaceholder`의 인스턴스로 작업해야한다.
    
- PHObject Class는 localIdentifier 프로퍼티에 따라 isEqual(_:) 및 해시 메소드를 구현한다

    - 이러한 메소드를 사용하여 asset 및 collection 객체를 추적 할 수 있다
    
- - -

### PHAsset

- class

    - A representation of an image, video, or Live Photo in the Photos library

- PHAsset은 사용자의 사진 라이브러리에 있는 하나의 asset을 나타내며, 해당 asset의 메타데이터를 제공한다

- `PHObjcet의 하위클래스`

- asset을 가져와 작업을 함

- Fetching Assets에 나열된 클래스 메소드를 사용하여 표시하거나, 수정하려는 asset을 나타내는 하나 이상의 PHAsset 인스턴스를 가져온다

    - Fetching Assets : Retrieve asset metadata or request full asset content
    
    - [Apple Developer - Docs about Fetching Assets](https://developer.apple.com/documentation/photokit/phasset/fetching_assets)
    
- asset은 메타데이터만 포함된다

- 특정 asset의 기본 이미지 또는 비디오 데이터가 로컬 디바이스에 저장되지 않을 수 있다

    - 그러나 이 데이터를 어떻게 사용 할 건지에 따라, 모든 데이터를 다운로드 할 필요가 없을 수도 있다
    
    - 예를 들어 썸네일 이미지로 collectionView를 채울 필요가 있는 경우, Photos 프레임워크는 각 asset의 썸네일을 다운로드, 생성 및 캐싱 할 수 있다, 자세한 내용은 PHImageManager 참고
    
    - PHImageManager : An object that facilitates retrieving or generating preview thumbnails and asset data.
    
    - [Apple Developer - Docs about PHImageManager](https://developer.apple.com/documentation/photokit/phimagemanager)
    
- Asset 객체를 변경 할 수 없다.

- asset의 메타데이터(예: 즐겨찾는 사진으로 표시)를 편집하려면, 사진 라이브러리 변경 블록 내에 PHAssetChangeRequest 객체를 만든다

    - PHAssetChangeRequest : A request to create, delete, change metadata for, or edit the content of a Photos asset, for use in a photo library change block.
    
    - [Apple Developer - Docs about PHAssetChangeRequest](https://developer.apple.com/documentation/photokit/phassetchangerequest)

- 변경 요청을 사용하고, 블록을 변경하여 사진 라이브러리를 업데이트 하는 방법은 PHPhotoLibrary 참고

    - PHPhotoLibrary : A shared object that manages access and changes to the user's shared photo library
    
    - [Apple Developer - Docs about PHPhotoLibrary](https://developer.apple.com/documentation/photokit/phphotolibrary)
    
- `즉, asset을 바로 직접 변경하는 것을 불가능, "변경  요청 객체"를 만들어서 요청해서 업데이트 하는 방법 밖에 없다`

- - -

### PHCollection

- class

    - The abstract superclass for Photos asset collections and collection lists.
    
- asset collections은 PHAssetCollection 클래스로 표시된다

- 하나의 asset collection은 사진 라이브러리 앨범이나, moment일 뿐만 아니라, 스마트 앨범 중 하나일 수 잇다

- PHAssetCollection은 PHCollection의 하위클래스이다.

- PHCollection은 asset collection을 위한 추상 슈퍼클래스이다

- PHObject를 상속받고 있다

- PHObject와 마찬가지로, PHCollection의 인스턴스를 직접 만들거나 이 인스턴스로 작업하면 안된다

    - 대신 PHAssetCollection또는 PHCollectionList라는 두개의 구체적인 하위 클래스 중 하나를 사용해야 한다.
    
- `PHAssetCollection객체`
    
    - 앨범, Moment 또는 공유사진 스트림과 같은 사진 또는 비디오 asset의 collection을 나타낸다

- `PHCollectionList객체`

    - 앨범이 포함된 폴더 또는 한 해의 모든 moment 집합과 같은 `다른 collection을 포함하는 collection`
    
- `중요`

    - 사진 라이브러리에 접근하더나 수정하려면 사용자의 명시적인 승인이 필요하다
    
    - Fetching Collections에 나열된 방법 중 하나를 호출하면 사진이 자동으로 사용자에게 승인을 요청하는 메시지를 표시한다
    
        - [Apple Developer - Docs about PHCollection의 Fetching Collections](https://developer.apple.com/documentation/photokit/phcollection#1656265)
        
    - 또는 PHPhotoLibrary requesetAuthorization(_:) 메소드를 사용하여 원하는 시간에 사용자에게 메시지를 보낼 수 있다
    
    - 앱의 info.plist 파일은 앱이 사진 접근을 요청하는 이유를 사용자에게 설명하는NSPhotoLibraryUsageDescription key 값을 제공해야 한다, key 가 없으면 앱이 crash 된다.
    
        - NSPhotoLibraryUsageDescription : A message that tells the user why the app is requesting access to the user;s photo library
        
        - Name : Privacy - Photo Library Usage Description, Type: String
        
        - [Apple Developer - Docs about NSPhotoLibraryUsageDescription](https://developer.apple.com/documentation/bundleresources/information_property_list/nsphotolibraryusagedescription)

- - -

### PHAssetCollection

- class

    - A representation of Photos asset grouping, such as a moment, user-creared album, or smart album
    
- Moment, 사용자 제작 앨범 또는 스마트 앨범과 같은 Photo asset 그룹의 표현이다

- PHCollection의 하위 클래스

- Photos framework에서 collection 객체(asset collections포함)는 해당 구성원 객체를 직접 참조하지 않는다

- collection객체를 직접 참조하는 다른 객체는 없다

- asset collections의 멤버를 검색하려면 fetchAssets(: options :)와 같은 PHAsset 클래스 메소드를 사용한다

- asset collections을 찾으려면 Fetching Asset Collections에 나열된 메소드 중 하나를 사용

    - [Apple Developer - Docs about Fetching Asset Collections](https://developer.apple.com/documentation/photokit/phassetcollection#1656287)

- 사용자의 명시적인 승인 필요

- asset과 collection lists와 마찬가지로, asset collections는 변경 불가

- asset collections를 생성, 이름 변경 또는 삭제하거나 asset collections에 구성원 추가, 제거 또는 재정렬하려면 사진 라이브러리 변경 블록 내에 PHAssetCollectionChangeRequest 객체를 만든다

    - 변경 요청을 사용하고 블록을 변경하여 사진 라이브러리를 업데이트 해야한다
    
    - 자세한 내용은 PHPhotoLibrary 참고
    
        - PHPhotoLibrary : A shared object that manages access and changes to the user's shared photo library
        
        - [Apple Developer - Docs about PHPhotoLibrary](https://developer.apple.com/documentation/photokit/phphotolibrary)

- - -

### PHCollectionList

- class

    - A group containing Photos asset collections, such as Moments, Years, or folders of uesr-created albums
    
- asset collections의 모음 이라고 생각하면 된다

- PHCollection의 하위 클래스

- Photos framework에서 collection객체(asset collection포함)는 해당 구성원 객체를 직접 참조하지 않는다

- collection 객체를 직접 참조하는 다른 객체는 없다

- collection list의 멤버를 검색하려면 fetchCollections(in: options:)와 같은 PHCollection 클래스 메소드를 사용하여 가져온다

- 상위 폴더가 없는 앨범 폴더와 같은 collection list 계층의 루트에서 객체를 찾으려면 fetchTopLevelUserCollections(with:)메소드를 사용한다

- 사용자의 명시적인 승인 필요

- collection list를 생성, 이름 변경 또는 삭제, collection list에 멤버를 추가, 제거 또는 재정렬 하려면 사진 라이브러리 변경 블록내에 PHCollectionListChangeRequest 객체를 만든다

    - 변경 요청을 사용하고 블록을 변경하여 사진 라이브러리를 업데이트
    
    - 자세한 내용은 PHPhotoLibrary 참고
    
        - PHPhotoLibrary : A shared object that manages access and changes to the user's shared photo library
        
        - [Apple Developer - Docs about PHPhotoLibrary](https://developer.apple.com/documentation/photokit/phphotolibrary)
        
- - -

### PHPhotoLibrary

- class

    - A shared object that manages access and chages to the user's shared photo library
    
- 사용자의 공유 사진 라이브러리 접근 및 변경을 관리하는 shared 객체

- NSObject의 하위 클래스

- shared PHPhotoLibrary객체는 로컬 디바이스에 저장된 asset과(활성화 된 경우) iCould Photos에 저장된 asset을 포함하여 사진앱에서 관리하는 전체 asset 및 collection 집합을 나타낸다

- PHPhotoLibrary 객체는 다음 작업에 사용된다

    - 앱이 사진 컨텐츠에 접근 할 수 있는 사용자 권한을 얻거나 확인
    
    - asset 및 collection을 변경
    
        - 예를들어, asset 메타데이터 또는 콘텐츠 편집, 새 asset 삽입 또는 collection 구성원 재배치
        
    - 라이브러리가 변경 할 때 전송된 업데이트 메세지 등록
- - -

### 용어 정리

- Assets: Image, Videos and Live Photos

- Collections of assets: Albums or Moments

- Lists of collections: Album folders or Moment clusters

    - 위 클래스 인스턴스는 읽기전용 (read-only), 변경 불가, 메타데이터만 포함

- - -

### PHFetchResult

- Generic Class

    - An orderd list of assets or collections returned from a Photos fetch method
    
- fetch method에서 반환된 asset또는 collection의 정렬된 list

- PHAsset, PHCollection, PHAssetCollection 및 PHCollectionList 클래스의 클래스 메소드를 사용하여 객체를 검색(retrieve)하면, Photos는 결과 객체를 fetch result에 제공한다

- fetch result의 내용은 NSArray 클래스에서 사용하는 것과 동일한 메소드 및 convention을 사용하여 접근한다

- 그러나 NSArray객체와 달리, PHFetchResult객체는 필요에 따라 Photos 라이브러리에서 내용을 동적으로 로드하므로 많은 수의 결과를 처리할 때도 최적의 성능을 제공한다

- fetch result는 내용에 대한 thread-safe한 접근을 제공한다

- fetch 후에 fetch result의 카운트 값은 일정하며 fetch result의 모든 객체는 동일한 localIdentifier을 유지한다.

    - 업데이트 된 컨텐츠를 가져오려면 shared PHPhotoLibrary 객체에 change observer를 등록
    
- fetch result는 컨텐츠를 캐시하여, 객체 한 묶음(batch)을 가장 최근에 엑세스한 인덱스 주위에 유지한다

- 배치 외부의 객체는 더이상 캐시되지 않으므로 이러한 객체에 접근하면 해당 객체를 다시 가져올 수 있다

    - 이 프로세스를 수행하면 해당 객체에서 이전에 읽은 값이 변경 될 수 있다.
    
- - -

