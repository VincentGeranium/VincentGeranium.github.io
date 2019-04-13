---
layout: post
title:  "TableViewLifeCycle Code Review"
date:   2019-04-13
categories: Swift
---

# TableViewLifeCycle Code Review

---

이번에도 코드를 읽어가며 공부를 해봅시다!!

전체 코드는 맨아래 있으니 참고하세요 !!

---

이번에는 코드를 통해 테이블 뷰의 라이프 사이클을 알아보자

```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
    cell.textLabel!.text = "Cell \(indexPath.row)"
    print("cellForRowAt : \(indexPath.row)") // 셀을 새로 생성할때마다 계속 찍히는 출력문
    return cell
  }
```

위의 메소드는 UITableViewDataSource 프로토콜의 메소드 이다

tableView 메소드는 **셀이 테이블 뷰의 특정 위치에 삽입 되도록 데이터 소스에 요청** 하는 메소드 이다

위 메소드의 파라미터는 2개가 있는데 tableView,indexPath 이다

먼저 tableView 파라미터는 **셀을 요청하는 테이블 뷰**를 받는다

그 다음 indexPath 파라미터는 **테이블 뷰에서 row(행)을 찾는 index 경로**를 받는다

**리턴으로는 테이블 뷰가 지정된 행에 사용할 수 있는 UITableViewCell에서 상속되는 객체**를 리턴한다

이 메소드 안에 있는 let cell을 뜯어보자 이 cell 상수는 위의 코드에서 보이듯이

**tableView 메소드의 리턴값**이 된다 
즉, 이 cell 상수는 **UITableViewCell** 에서 상속되는 객체이다

그리고 이 cell 을 뜯어보면 다음과 같다

```
let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
```

이 코드를 한번 읽어보면

이 cell 상수는 **dequeueReusableCell 메소드의 반환값**을 받는다

다시말해 **tableView 메소드의 리턴값은 dequeueReusableCell 메소드인 cell 인 것이다**

이 dequeueReusableCell 메소드는 **지정된 재사용 식별자 (identifier)에 대한 재사용 가능한 테이블 뷰의 셀 객채를 반환하고 테이블 뷰에 추가** 하는 기능을 하며

cell 상수는 **dequeueReusableCell 메소드의 리턴 값인 identifier 가 같은 UITableViewCell 객체, 유효한 셀을 받는 것이다**를 받는 것이다

그래서

```
print("cellForRowAt : \(indexPath.row)")
```

코드를 넣어 시뮬레이터를 실행시켜 셀을 위 아래로 움직이는 액션을 주면 테이블 뷰에서 새로 생성되는 IndexPath 의 row 값을 출력해서 볼 수 있다

**참고** : **struct IndexPath는 중첩 배열 트리의 특정 위치에 대한 경로를 함께 나타내는 인덱스 목록이다**

```
extension TableViewLifeCycle: UITableViewDelegate {
    func tableView(_ tableView: UITableView, willDisplay cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Will Display Cell : \(indexPath.row)")
    }
    func tableView(_ tableView: UITableView, didEndDisplaying cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Did End Display Cell : \(indexPath.row)"
```

이번에는 UITableViewDelegate 프로토콜 내에 구현된 메소드들을 살펴보자

```
func tableView(_ tableView: UITableView, willDisplay cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Will Display Cell : \(indexPath.row)")
    }
```

이 메소드는 **테이블 뷰가 특정 행에 대해 셀을 새로 만들어 내려고 한다는 것을 delegate에게  알려준다** 이러한 역활을 한다 그러므로 이 메소드는 내에 

```
 print("Will Display Cell : \(indexPath.row)")
```

이 출력문 코드는 새로 셀이 만들어 내려고 할 때 IndexPath의 row 값을 출력해서 볼 수 있다

```
func tableView(_ tableView: UITableView, didEndDisplaying cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Did End Display Cell : \(indexPath.row)")
```

이 메소드는 **지정된 셀이 테이블에서 제거되엇다는 것을 delegate에게 알려주는** 역활을 한다

**즉, 지정된 셀이 테이블에서 제거되는 시점에 대한 것** 그래서 그때에 행동할 코드를 넣어 주면 되는데

```
 print("Did End Display Cell : \(indexPath.row)")
```

위의 출력문을 이용하여 **제거가 되는 셀의 row 값을 출력한다**

---

# Code

```
import UIKit

final class TableViewLifeCycle: UIViewController {
  
  override var description: String {
    return "TableView - LifeCycle"
  }
  let data = Array(1...40)
  
  override func viewDidLoad() {
    super.viewDidLoad()
    let tableView = UITableView(frame: view.frame)
    tableView.dataSource = self
    tableView.delegate = self
    tableView.register(MyTableViewCell.self, forCellReuseIdentifier: "CellId")
    view.addSubview(tableView)
  }
}

extension TableViewLifeCycle: UITableViewDataSource {
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return data.count
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
    cell.textLabel!.text = "Cell \(indexPath.row)"
    print("cellForRowAt : \(indexPath.row)") 
    return cell
  }
}
extension TableViewLifeCycle: UITableViewDelegate {
    func tableView(_ tableView: UITableView, willDisplay cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Will Display Cell : \(indexPath.row)")
    }
    func tableView(_ tableView: UITableView, didEndDisplaying cell: UITableViewCell, forRowAt indexPath: IndexPath) {
        print("Did End Display Cell : \(indexPath.row)") 
    }
}

```
