---
layout: post
title:  "2019-11-16-Table-View-Cell-Study-Summary"
date:   2019-11-16
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 테이블뷰 셀](https://www.edwith.org/boostcourse-ios/lecture/16886/)

- - -

### What is TableView Cell ??

- 테이블뷰 셀(TableView Cell)은 테이블뷰를 이루는 개별적인 행(row)으로, UITableViewCell 클래스를 상속받는다.

- UITableViewCell 클래스에 정의된 표준 스타일을 활용해 문자열 혹은 이미지를 제공하는 셀을 생성할 수 있다.

- 커스텀 서브뷰를 올려 다양한 시각적 모습을 나타낼 수 있다

- - -

### 테이블뷰 셀의 구조

- 기본적으로 테이블뷰 셀은 크게 콘텐츠 영역과 액세서리뷰 영역으로 구조가 나뉜다

![tableViewCellImag-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellImag-1.png?raw=true)

- 콘텐츠 영역: 셀의 왼쪽 부분에는 주로 문자열, 이미지 혹은 고유 식별자 등이 입력된다
    
- 엑세서리뷰 영역: 셀의 오른쪽 작은 부분은 엑세서리뷰로 상세보기, 재정렬, 스위치 등과 같은 컨트롤 객체가 위치한다.

![tableViewCellImag-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellImag-2.png?raw=true)

- - -

### 테이블뷰를  편집 모드(Editing Mode)로 전환시 셀의 구조

- 편집 컨트롤은 삭제 컨트롤(빨간색 원 안에 마이너스 기호) 또는 추가 컨트롤(녹색 원 안에 플러스 기호) 중 하나가 될 수 있다.

- 재정렬이 가능한 경우, 재정렬 컨트롤이 액세서리뷰에 나타난다.

- 재정렬 컨트롤을 눌러 셀을 드래그하면 위아래로 순서를 변경할 수 있다

![tableViewCellEditingModeImg-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellEditingModeImg-2.png?raw=true)

![tableViewCellEditingModeImg-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellEditingModeImg-1.png?raw=true)

![tableViewCellEditingModeImg-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellEditingModeImg-3.png?raw=true)

- - -

### 테이블뷰 셀의 기본 기능

- UITableViewCell 클래스를 상속받는 기본 테이블뷰 셀은 표준 스타일을 이용할 수 있다

    - 표준 스타일의 콘텐츠 영역은 한 개 이상의 문자열 그리고 이미지를 지닐 수 있다

    - 이미지가 오른쪽으로 확장됨에 따라 문자열이 오른쪽으로 밀려난다
    
![tableViewCellBasicFunctionImg-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellBasicFunctionImg-1.png?raw=true)

- UITableViewCell 클래스는 셀 콘텐츠에 세 가지 프로퍼티가 정의되어 있다

    - textLable: UILabel -> 주제목 레이블
    
    - detailTextLabel: UILabel -> 추가 세부 사항 표시를 위한 부제목 레이블
    
    - imageView: UIImageView -> 이미지 표시를 위한 이미지뷰
    
![tableViewCellBasicFunctionImg-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/tableViewCellBasicFunctionImg-2.png?raw=true)

- - -

### 커스텀 테이블뷰 셀

- UITableViewCell 클래스에서 제공하는 표준 스타일 셀을 이용해 이미지와 문자열을 표현하고 글꼴 및 색상 등을 수정할 수 있다

    - 그러나 기본 형태를 벗어나 다양한 애플리케이션의 요구를 충족시키기 위해 셀을 커스텀 할 수 있다.
    
    - 셀을 커스텀 하면 이미지를 텍스트 오른쪽에 위치시키는 등 원하는 시각적 형태를 만들 수 있다.
    
- 셀을 커스텀 하는 방법에는 크게 두 가지 방법이 있는데 그 두s가지 방법을 스토리보드를 이용하거나 코드로 구현할 수 있다

- 셀을 커스텀 하는 대표적 방법 두 가지

    - 1. 셀의 콘텐츠뷰에 서브뷰 추가하기
    
    - 2. UITableViewCell의 커스텀 서브클래스 만들기
    
- - -

### 참고사항

- UITableViewCell의 서브클래스를 이용해 커스텀 이미지뷰를 생성하는 경우, 이미지뷰의 변수명을 imageView로  명명하면 기본 이미지뷰 프로퍼티와 변수명이 같아 원하는 대로 동작하지 않을 수 있다

    - 반드시 커스텀 이미지뷰의 변수명은 다르게 지어주어야 한다
    
    - textLabel, detailLabel, accessoryView 등의 기본 프로퍼티 이름 모두 마찬가지이다.