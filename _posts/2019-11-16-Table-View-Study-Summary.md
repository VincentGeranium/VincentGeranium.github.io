---
layout: post
title:  "2019-11-16-Table-View-Study-Summary"
date:   2019-11-16
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 테이블 뷰](https://www.edwith.org/boostcourse-ios/lecture/16860/)

- - -

### What is TableView ??

- 테이블뷰는 iOS 애플리케이션에서 많이 활용하는 사용자 인터페이스

- 테이블뷰는 `리스트 형태`를 지니고 있으며 `스크롤이 가능`해 `많은 정보를 보여 줄 수 있다.`

- - -

### 테이블뷰 기본 형태

- 테이블뷰는 하나의 열(column)과 여러 줄의 행(row)을 지난다

- 테이블뷰는 수직으로만 스크롤이 가능하다

- 각 행은 하나의 셀(cell)에 대응한다

- 섹션(section)을 이용해 행을 시각적으로 나눌 수 있다

- 헤더(header)와 풋터(footer)에 이미지나 텍스트를 추가해 추가 정보를 보여줄 수 있다

![ta1bleViewImg-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ta1bleViewImg-1.png?raw=true)

![tableViewImg-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ta1bleViewImg-2.png?raw=true)

- - -

### 테이블뷰 스타일

- 테이블뷰는 크게 두 가지 스타일(일반, 그룹)으로 나뉜다

- - -

### 일반 테이블뷰(Plain TableView)

- 더 이상 나뉘지 않는 연속적인 행의 리스트 형태이다

- 하나 이상의 섹션을 가질 수 있으며, 각 섹션은 여러 개의 행을 지닐 수 있다.

- 각 섹션은 헤더 혹은 푸터를 옵션으로 지닐 수 있다

- 색인을 이용한 빠른 탐색을 하거나 옵션을 선택할 때 용이하다

![plainTableViewImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/plainTableViewImg.png?raw=true)

- - -

### 그룹 테이블뷰(Grouped TableView)

- 섹션을 기준으로 그룹화되어있는 리스트 형태

- 하나 이상의 섹션을 가질 수 있으며, 각 섹션은 여러 개의 행을 지닐 수 있다

- 각 섹션은 헤더 혹은 푸터를 옵션으로 지닐 수 있다

- 정보를 특정 기준에 따라 개념적으로 구분할 때 적합하다

- 사용자가 정보를 빠르게 이해하는 데 도움이 된다.

![groupedTableViewImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/groupedTableViewImg.png?raw=true)

- - -

### 테이블뷰 생성

- 테이블뷰를 생성하고 관리하는 좋은 방법은 스토리보드에서 커스텀 UITableViewController 클래스의 객체를 이용하는 것이다

    - 필요에 따라서 소스코드로 테이블뷰를 생성하는 것도 가능하다
    
- 스토리보드에서 테이블뷰의 특성을 지정할 때, 동적 프로토타입(dynamic prototypes)혹은 정적 셀(static cells)중 하나를 선택 할 수 있다

    - 새로운 테이블뷰를 생성할 때 기본 설정 값은 동적 프로토타입이다
- - -

### 동적 프로토타입(Dynamic Prototypes)

- 셀 하나를 디자인해 이를 다음 셀의 템플릿으로 사용하는 방식

- 같은 레이아웃의 셀을 여러 개 이용해 정보를 표시할 경우 사용

- 데이터 소스(UITableViewDataSource) 인스턴스에 의해 콘텐츠를 관리하며, 셀의 개수가 상황에 따라 변하는 경우에 사용

- - -

### 정적 셀(Static Cells)

- 고유의 레이아웃과 고정된 수의 행을 가지는 테이블뷰에 사용

- 테이블뷰를 디자인하는 시점에 테이블의 형태와 셀의 개수가 정해져 있는 경우 사용

- 셀의 개수가 변하지 않음

- - -