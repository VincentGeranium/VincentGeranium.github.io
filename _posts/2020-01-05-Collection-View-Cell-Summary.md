---
layout: post
title:  "Collection View Cell Summary"
date:   2020-01-05
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - Collection View Cell](https://www.edwith.org/boostcourse-ios/lecture/16907/)

- - -

### 컬렉션뷰 셀의 특징

- 컬렉션뷰 셀은 데이터 아이템을 화면에 표시.

- 하나의 셀은 하나의 데이터 아이템을 화면에 표시.

- 컬렉션뷰 셀은 두 개의 배경을 표시하는 뷰와 하나의 콘텐츠를 표시하는 뷰로 구성되어 있다.

    - 두 개의 배경뷰는 셀이 선택되었을 때 사용자에게 시각적인 표현을 제공하기 위해 사용된다.
    
- 셀의 레이아웃은 컬렉션뷰의 레이아웃 객체에 의해 관리된다.

- 컬렉션뷰 셀은 뷰의 재사용 메커니즘을 지원한다.

- 일반적으로 컬렉션뷰 셀 클래스의 인스턴스는 직접 생성하지 않는다.

    - 대신 특정 셀의 하위 클래스를 컬렉션뷰 객체에 등록한 후, 컬렉션뷰 셀 클래스의 새로운 인스턴스가 필요할 때, 컬렉션의 dequeueReusableCell(withReuseIdentifier:for:) 메서드를 호출한다
    
        - 스토리보드를 사용하여 셀을 구성하면 컬렉션뷰에 따로 셀 클래스를 등록할 필요는 없다
        
- - -

### UICollectionViewCell 클래스

#### 컬렉션뷰 셀의 구성요소 관련 프로퍼티

- var contentView: UIView
    
    - 셀의 콘텐츠를 표시하는 뷰.
    
- var backgroundView: UIView?

    - 셀의 배경을 나타내는 뷰.
    
    - 이 프로퍼티는 셀이 처음 로드되었을 경우와 셀이 강조 표시되지 않거나 선택되지 않을 때 항상 기본 배경의 역활을 한다.
    
- var selectedBackgroundView: UIView?

    - 셀이 선택되었을 때 배경뷰 위에 표시되는 뷰.
    
    - 이 프로퍼티는 셀이 강조 표시되거나 선택될 때마다 기본 배경 뷰인 backgroundView를 대체하여 표시된다.
    
#### 컬렉션뷰 셀의 상태 관련 프로퍼티

- var isSelected: Bool

    - 셀이 선택되었는지를 나타낸다.
    
    - 셀이 선택되어있지 않는다면 이 프로퍼티의 값은 false.
    
- var isHighlighted: Bool

    - 셀의 하이라이트 상태를 나타낸다.
    
    - 하이라이트 되어있지 않는다면 기본 값은 false.
    
#### 컬렉션뷰 셀의 드래그 상태 관련 메서드

- func dragStateDidchange(_:)

    - 셀의 드래그 상태가 변경되면 호출된다
    
        - 드래그 상태는 UICollectionViewCellDragState의 열거형으로 표현되고 none, lifting, dragging의 3가지 상태를 갖는다
    
- - -

### 컬렉션뷰 셀 vs 테이블뷰 셀

#### 컬렉션뷰 셀과 테이블뷰 셀의 차이점

- 테이블뷰 셀의 구조는 콘텐츠 영역과 액세서리뷰 영역으로 나뉘었지만, 컬렉션뷰 셀은 배경뷰와 실제 콘텐츠를 나타내는 콘텐츠뷰로 나뉘어있다.

- 테이블뷰 셀은 기본으로 제공되는 특정 스타일을 적용할 수 있지만 컬렉션뷰 셀은 특정한 스타일이 따로 없다.

- 테이블뷰 셀은 목록형태로만 레이아웃 되지만, 컬렉션뷰 셀은 다양한 레이아웃을 지원한다.

- - -