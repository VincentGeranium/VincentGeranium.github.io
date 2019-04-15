---
layout: post
title:  "TableView List Method 공부 - 190415"
date:   2019-04-15
categories: Swift, iOS
---

# TableView Code

---

각 코드에 나와있는 메소드들이나 모르는 것들만 선택적으로 해석하고 알아보는 시간을 가져보려 합니다

---

tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")

위의 코드에 사용된 메소드를 알아봅시다!!

```
func register(_ cellClass: AnyClass?, forCellReuseIdentifier identifier: String)
```

위의 코드에 사용된 메소드 입니다

먼저 Quick Help에 나와있는 summary를 봐 봅시다

summary에는 **새로운 표의 셀을 만드는 데 사용할 클래스를 등록합니다** 라고 나와있네요

그렇다면 즉, 이 메소드는 새로운 표의 셀을 만드는 데 사용할 클래스를 등록하는 기능을 하는것이네요!!

그런데 여기서 중요한 점이 있어요, 이 메소드는 그냥 사용하는 메소드가 아니라 UITableViewDataSource 에서 꼭 구현해야만 하는 메소드에요

다시 한번 봐 볼까요??

```
extension ListViewController: UITableViewDataSource {
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return viewControllers.count
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
  }
}
```

이 전체 코드를 보면 알듯이 ListViewController은 final class 이고, 이 클래스를 extension 하여 UITableViewDataSource이 가지고 있는 기능(메소드)를 선택하여 ListViewController에서 구현하는 것인데 UITableViewDataSource를 확장하여 사용하려면 꼭 2가지의 메소드를 구현해야 해요

UITableViewDataSource의 Definition을 봐보면 다른 메소드들은 optional로 되어있지만 두개는 optional이 붙어있지 않아요 그래서 꼭 2가지는 구현해야 합니다

그게 바로 위에 코드에 나와있는 메소드에요

그렇다면 UITableViewDataSource에서 꼭 구현해야 할 메소드 중 첫번째를 뜯어볼까요??

먼저 첫번째 메소드의 정의를 봐봅시다

```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
```

첫번째 메소드의 정의는 위와 같은데 이 메소드의 summary를 봐봐야지 어떻게 어디에서 사용되는지 알겟죠?? 이 메소드의 quick help를 들어가서 summary를 봐봅시다

이 메소드의 summary에는 **테이블 뷰에 지정된 섹션에 있는 행(row)의 수를 반환하도록 데이터 소스에 지시합니다** 라고 나와있네요

그럼 이 메소드의 파라미터와 리턴을 알아봐야 겠네요, 그래야 이 메소드의 정확한 구동 방식을 알고 다음에 또 사용할 수 있겠죠??

먼저 이 메소드에는 2가지의 파라미터를 받는데요 그 두 가지의 파라미터는 위의 정의 코드를 보면 알 수 있듯이 **tableView: UITableView와 section: Int** 가 있고, 리턴 타입으로는 Int 타입의 값을 반환 받도록 하네요

그럼 두 가지의 파라미터가 각각 어떠한 값을 받는지 알아볼까요??

먼저 tabelView 파라미터를 봅시다.

이 파라미터는 UITableView 타입을 파라미터 값으로 받네요

그리고 이 파라미터에 들어오는 값은 quick help에서 보면 **이 정보를 요청하는 테이블 뷰 객체 입니다** 라고 나와 있네요

아하! 그럼 이 파라미터에는 **테이블 뷰에 지정된 섹션에 있는 행의 수 정보를 요청하는 테이블 뷰 객체**가 들어가야 겠네요

그럼 두 번째 파라미터인 section: Int 를 보면 더욱더 이 메소드에 대한 이해가 높아질거 같아요

그럼 한번 봐 볼까요??

두 번째 파라미터인 section: Int는 **테이블 뷰의 인덱스 섹션을 구분(식별)하는 번호** 라고 나와있네요

아 그럼 이 파라미터에 들어오는 값은 각 섹션을 구분해주는 번호를 넣으면 되겠네요

뭔가 알기 어렵네요 조금 더 알아볼까요??

먼저 이 파라미터의 section의 default 값을 알아야해요

이 파라미터의 section의 default 값은 1로 지정이 되어있어서 만약에 지정을 해주지 않는다면 section은 한개가 되겠네요

그럼 3으로 한다면?? section의 갯수는 3이 되겠죠?? 왜냐하면 **이 section 파라미터는 테이블 뷰의 인덱스 섹션을 구분(식별)해 주는 번호이니까요**

마지막으로 리턴값을 알아볼까요??

리턴값은 **섹션의 행의 갯수**를 반환한다고 나와 있네요 그럼 리턴값에 12를 주면 12개의 행이 생성되겠네요?!

여기서 알아야 할 점이 있는데 **섹션과 행 즉, Section 과 Row는 다르다는 것을 꼭 인지하고 있어야 합니다!!** 

그럼 이 메소드를 종합적으로 예를들어 이해하기 쉽게 알아보죠

일단 이 메소드는 dataSource의 꼭 구현하야 할 메소드입니다.

그리고 이 dataSouce는 delegate 처럼 어디서 구현을 할 것인지 지정을 하고 그곳에서 dataSource 내에서 구현한 메소드들을 구현하죠 (tableView.dataSource = self)

그럼 이 dataSouce를 어디서 동작하는지 알았내요 그럼 이 안에 꼭 구현해야 할 메소드 중 우리는 첫번째 메소드를 공부하고 있으니 이 첫번째 메소드가 이 클래스 내에서 구현 된다는 것을 알고 있어요

이 첫번째 메소드의 파라미터 중 tableView: UITableView 를 받는다고 나와있는데 우리는 파라미터 값을 넣어준 적이 없죠??

그런데 이 메소드가 동작을 해요. 왜 그럴까요?? 바로 dataSource의 특징 때문이에요.

바로 앞에서 말했는데 dataSource는 어디서 구현할 것인지 지정해주어야 한다고 했죠?? 우리는 지정을 했어요

```
tableView.dataSource = self
```

바로 이 코드로 말이죠 그래서 UITableView 타입인 

```
let tableView = UITableView()
```

가 파라미터 값으로 들어가게 되고 이 상수값은 지금 코드의 클래스 내에 구현이 되어있습니다

저는 이 전체 코드를 보면서 가장 어려웠던것이 **IndexPath**에 대한 개념이였어요

이 IndexPath 에 대한 공부는 이 다음에 다시 해서 올리도록 할게요 오늘은 여기까지 입니다!!

---

```
import UIKit

final class ListViewController: UIViewController {
  let tableView = UITableView()
  var viewControllers: [UIViewController] = []
  
  override func viewDidLoad() {
    super.viewDidLoad()
    tableView.frame = view.frame
    tableView.delegate = self
    tableView.dataSource = self
    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")
    view.addSubview(tableView)
  }
  
  override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    viewControllers = [
      TableViewNumbers(),
      TableViewSection(),
      TableViewRefresh(),
      TableViewMultipleSelection(),
      TableViewAccessoryType(),
    ]
  }
}


// MARK: - UITableViewDataSource

extension ListViewController: UITableViewDataSource {
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return viewControllers.count
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
  }
}

// MARK: - UITableViewDelegate

extension ListViewController: UITableViewDelegate {
  func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let vc = viewControllers[indexPath.row]
    navigationController?.pushViewController(vc, animated: true)
  }
}
```

---

