---
layout: post
title:  "Collection View ?"
date:   2020-01-04
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Collection View](https://www.edwith.org/boostcourse-ios/lecture/16906/)

- - -

### What is Collection View

- iOS 애플리케이션에서 컬렉션뷰는 그리드와 스택, 타일, 그리고 원형 배열을 포함하여 다양한 유연성을 제공하는 인터페이스

- 컬렉션뷰는 유연하고 변경 가능한 레이아웃을 사용하여 데이터 아이템의 정렬된 세트를 표시하는 수단

- 컬렉션뷰의 가장 일반적인 용도는 데이터 아이템을 그리드와 같은 형태로 표현

- 더불어 다양한 방법으로 컬렉션뷰의 레이아웃을 사용자 정의할 수 있다

![collectioViewImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/collectioViewImage-1.png?raw=true)

- - -

### 컬렉션뷰의 구성요소

![collectioViewImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/collectioViewImage-2.png?raw=true)

- 셀(Cell)

    - 컬렉션뷰의 주요 콘텐츠를 표시.
    
    - 컬렉션뷰는 컬렉션뷰 데이터 소스 객체에서 표시할 셀에 대한 정보를 가저온다.
    
    - 각 셀은 UICollectionViewCell 클래스의 인스턴스 또는 UICollectionViewCell을 상속받은 클래스 인스턴스 이다.
    
- 보충 뷰(Supplementary views)

    - 섹션에 대한 정보를 표시한다
    
    - 셀과 달리 보충 뷰는 필수는 아니다
    
    - 사용법과 배치 방식은 사용되는 레이아웃 객체가 제어한다
    
    - 헤더와 푸터를 예로 들 수 있다
    
- 데코레이션 뷰(Decoration Views)

    - 콘텐츠가 스크롤 되는 컬렉션뷰에 대한 배경을 꾸밀 때 사용한다
    
    - 레이아웃 객체는 데코레이션 뷰를 사용하여 커스텀 배경 모양을 구현할 수 있다
    
- 레이아웃 객체(Layout Object)

    - 레이아웃 객체는 컬렉션뷰 내의 아이템 배치 및 시각적 스타일을 결정한다
    
    - 컬렉션뷰 데이터 소스 객체가 뷰와 표시할 콘텐츠를 재공한다면, 레이아웃 객체는 크기, 위치 및 해당 뷰의 레이아웃과 관련된 특성들을 결정한다
    
- - -

### 컬렉션뷰 구현을 이루기 위한 클래스 및 프로토콜

- 컬렉션뷰를 사용하여 콘텐츠를 화면에 표시하기 위해서 컬렉션뷰는 여러 가지 다른 객체들과 협력한다 

    - 예를 들어, 컬렉션뷰는 컬렉션뷰 데이터 소스 객체로부터 표시할 콘텐츠의 정보를 얻어오고, 사용자와의 상호작용을 처리하기 위해 컬렉션뷰 델리게이트 객체를 사용한다

- 최상위 포함 및 관리(Top level containment)

    - UICollectionView / UICollectionViewController
    
        - UICollectionView는 컬렉션뷰의 콘텐츠가 보이는 영역을 정의한다.
        
        - UICollectionViewController는 컬렉션뷰를 관리하는 뷰 컨트롤러이다. 
        
        - UICollectionViewController는 선택적으로 사용 가능하다.
        
- 콘텐츠 관리

    - UICollectionViewDataSource protocol / UICollectionViewDelegate protocol
    
        - 데이터 소스 객체는 컬렉션뷰와 관련된 중요한 객체이며, 필수적으로 제공해야한다.
        
        - 데이터 소스는 컬렉션뷰의 콘텐츠를 관리하고 해당 콘텐츠를 표시하기 위한 뷰를 제공한다.
        
        - 컬렉션뷰 델리게이트 객체는 사용자와의 상호작용과 셀 강조 표시 및 선택등을 관리한다.

- 표시(Presentation)

    - UICollectionReusableView / UICollectionViewCell
    
        - 컬렉션에 표시된 모든 뷰는 UICollectionReusableView 클래스의 인스턴스여야한다
        
        - 이 클래스는 컬렉션뷰에서 사용 중인 뷰 재사용 메커니즘을 지원한다
        
        - 새로운 뷰를 만드는 대신, 뷰를 재사용하여 성능을 향상시킨다
        
- 레이아웃(Layout)
    
    - UICollectionViewLayout / UICollectionViewLayoutAttribute / UICollectionViewUpdateItem
    
        - UICollectionViewLayout의 서브클래스는 레이아웃 객체라고 하며 컬렉션뷰 내부의 셀 및 재사용 가능한 뷰의 위치, 크기 및 시각적 속성을 정의한다
        
        - UICollectionViewLayoutAttributes는 레이아웃 프로세스 중에 컬렉션뷰에 셀과 재사용 가능한 뷰를 표시하는 위치와 방법을 알려준다
        
        - 레이아웃 객체 아이템의 삽입, 삭제, 혹은 컬렉션뷰 내에서 이동할 때마다 레이아웃 객체는 UICollectionViewUpdateItem 클래스의 인스턴스를 받는다
        
- 플로우 레이아웃(Flowlayout)

    - UICollectionViewFlowLayout / UICollectionViewDelegateFlowLayout protocol
    
        - 그리드 혹은 다른 라인기반(line-based) 레이아웃을 구현하는 데 사용된다
        
        - 클래스를 그대로 사용하거나 동적으로 커스터마이징 할 수 있는 플로우 델리게이트 객체와 함께 사용할 수 있다.

- - -

### 컬렉션뷰와 관련된 클래스 및 프로토콜

- UICollectionView : 사용자에게 보여질 컬렉션 형태의 뷰

- UICollectionViewCell : UICollectionView 인스턴스에 제공되는 데이터를 화면에 표시하는 역활을 담당

- UICollectionReusableView : 뷰 재사용 메커니즘을 지원한다

- UICollectionViewFlowLayout : 컬렉션뷰를 위한 디폴트 클래스로, 그리드 스타일로 셀들을 배치하도록 설계되어 있다. scrollDirection 프로퍼티를 통해 수평 및 수직 스크롤을 지원한다

- UICollectionViewLayoutAttributes : 컬렉션뷰 내의 지정된 아이템의 레이아웃 관련 속성을 관리

- UICollectionViewDataSource 프로토콜 : 컬렉션뷰에 필요한 데이터 및 뷰를 제공하기 위한 기능을 정의한 프로토콜

- UICollectionViewDelegate 프로토콜 : 컬렉션뷰에서 아이템의 선택 및 강조 표시를 관리하고 해당 아이템에 대한 작업을 수행할 수 있는 기능을 정의한 프로토콜

- UICollectionViewDelegateFlowLayout 프로토콜 : UICollectionViewLayout 객체와 함께 그리드 기반 레이아웃을 구현하기 위한 기능을 정의한 프로토콜
    