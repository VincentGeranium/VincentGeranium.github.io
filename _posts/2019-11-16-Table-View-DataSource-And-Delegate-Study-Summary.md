---
layout: post
title:  "2019-11-16-Table-View-DataSource-And-Delegate-Study-Summary"
date:   2019-11-16
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 테이블뷰 DataSource와 Delegate](https://www.edwith.org/boostcourse-ios/lecture/16887/)

- - -

### What is DataSource And Delegate ??

- UITableView 객체는 데이터 소스와 델리게이트가 없다면 정상적으로 동작하기 어려우므로 두 객체가 꼭 필요하다

- MVC 프로그래밍 디자인 패턴에 따라 데이터 소스는 애플리케이션의 데이터 모델(M)과 관련되어 있다

- MVC 프로그래밍 디자인 패턴에 따라 델리게이트는 테이블뷰의 모양과 동작을 관리하기에 컨트롤러(C)의 역활에 가깝다

- MVC 프로그래밍 디자인 패턴에 따라 테이블뷰는 뷰(V)의 역활을 한다

- 데이터 소스와 델리게이트 덕분에 테이블뷰를 매우 유연하게 만들 수 있다

![DataSourceAndDelegateImg-1]()

- - -

### DataSource

- 테이블뷰 데이터 소스 객체는 UITableViewDataSource 프로토콜을 채택한다

- 데이터 소스는 테이블 뷰를 생성하고 수정하는데 필요한 정보를 테이블뷰 객채에 제공한다

- 데이터 소스는 데이터 모델의 델리게이트로, 테이블뷰의 시각적 모양에 대한 최소한의 정보를 제공한다

- UITableView 객체에 섹션의 수와 행의 수를 알려주며, 행의 삽입, 삭제 및 재정렬하는 기능을 선택적으로 구현할 수 잇다

- - -

### UITableViewDataSource 프로토콜의 주요 메소드

- @required로 선언된 두 가지 메서드는 UITableViewDataSource 프로토콜을 채택한 타입에 필수로 구현해야 한다

```swift

@required
// 특정 위치에 표시할 셀을 요청하는 메서드
func tableView(UITableView, cellForRowAt: IndexPath)

// 각 섹션에 표시할 행의 개수를 묻는 메서드
func tableView(UITableView, numberOfRowsInSection: Int)

@optional
// 테이블뷰의 총 섹션 개수를 묻는 메서드
func numberOfSections(in: UITableView)

// 특정 섹션의 헤더 혹은 풋터 타이틀을 묻는 메서드
func tableView(UITableView, titlerForHeaderInSection: Int)
func tableView(UITableView, titleForFooterInSection: Int)

// 특정 위치의 행을 삭제 또는 추가 요청하는 메서드
func tableView(UITableView, commit: UITableViewCellEditionStyle, forRowAt: Index)

// 특정 위치의 행이 편집 가능한지 묻는 메서드
func tableView(UITableView, canEditRowAt: IndexPath)

// 특정 위치의 행을 재정렬 할 수 있는지 묻는 메서드
func tableView(UITableView, canMoveRowAt: IndexPath)

// 특정 위치의 행을 다른 위치로 옮기는 메서드
func tableView(UITableView, moveRowAt: IndexPath, to: IndexPath)

```
- - -

### UITableViewDelegate 프로토콜의 주요 메서드

- 테이블뷰 델리게이트 객체는 UITableViewDelegate 프로토콜을 채택한다

- 델리게이트는 테이블뷰의 시각적인 부분 수정, 행의 선택 관리, 액세서리뷰 지원 그리고 테이블뷰의 개별 행 편집을 도와준다

- 델리게이트 메서드를 활용하면 테이블뷰의 세세한 부분을 조정할 수 있다

```swift

// 특정 위치의 행의 높이를 묻는 메서드
func tableView(UITableView, heightForRowAt: IndexPath)

// 특정 위치의 행을 들여쓰기 수준을 묻는 메서드
func tableView(UITableView,indentationLevelForRowAt: IndexPath)

// 지정된 행의 선택되었음을 알리는 메서드
func tableView(UITableView, didSelectRowAt: IndexPath)

// 지정된 행의 선택이 해제되었음을 알리는 메서드
func tableView(UITableView, didDeselectRowAt: IndexPath)

// 특정 섹션의 헤더뷰 또는 풋터뷰를 요청하는 메서드
func tableView(UITableView, viewForHeaderInSection: Int)
func tableView(UITableView, viewForFooterInSection: Int)

// 특정 섹션의 헤더뷰 또는 풋터뷰를 높이를 물어보는 메서드
func tableView(UITableView, heightForHeaderInSection: Int)
func tableView(UITableView, heightForFooterInSection: Int)

// 테이블뷰가 편집모드에 들어갔음을 알리는 메서드
func tableView(UITableView, willBeginEditingRowAt: IndexPath)

// 테이블뷰가 편집모드에서 빠져나왔음을 알리는 메서드
func tableView(UITableView, didEndEditingRowAt: IndexPath?)

```