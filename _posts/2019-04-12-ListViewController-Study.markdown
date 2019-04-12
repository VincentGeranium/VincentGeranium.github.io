---
layout: post
title:  "ListViewController 공부"
date:   2019-04-12
categories: Swift, iOS
---

# ListViewController Code Review

---

![screenShot](https://user-images.githubusercontent.com/42841888/56043894-0ce0dd00-5d79-11e9-880e-daea464a3dee.png)

위의 그림과 같은 뷰를 나타내기 위해서 만든 코드를 하나씩 뜯어보면서 공부해보자
먼저, 클래스 안에 프로퍼티로 정의된 viewControllers를 보면 UIViewcController을 받는데 특이한 형태로 받는다

```
var viewControllers: [UIViewController] = []
```

위의 코드의 타입을 알고 싶어서 **type(of:viewControllers)** 를 해보면 **Array<UIViewController>** 라고 나온다
배열은 여러개의 값을 넣을 수 있는 컬렉션 타입 중 하나이다, 하나의 Array(배열)을 동일한 자료형을 갖는 값들로 구성하도록 하는 것이 일반적인데,

```
var someArray:[Any]
```

위와 같이 자료형을 Any 혹은 AnyObject 로 하면 여러자료형을 받을 수 있다.  
  
다시 본론으로 돌아와 viewControllers는 UIViewController 클래스를 Array받는다

```
  override func viewDidLoad() {
    super.viewDidLoad()
    tableView.frame = view.frame
    tableView.delegate = self
    tableView.dataSource = self
    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")
    view.addSubview(tableView)
  }
```

아래서도 말할것이지만 viewDidLoad는 ViewController의 생명주기와 관련이 있다
viewDidLoad는 view가 Load 된 직후에 호출 된다. 즉, **뷰의 컨트롤러가 메모리에 로드되고 난 후에 호출된다** 는 뜻이다.

그렇다면 뷰의 컨트롤러가 메모리에 로드되고 난 후의 할 일들을 이 메소드 안에 코드를 넣어주면 메모리에 로드되고 난 후에 그 코드들이 실행된다고 생각하면 된다
그러나 주의해야 할 점이 있다 앱을 실행하고 난 후에 viewDidLaod 메소드는 딱 한번만 실행이 된다.

그리고 ViewDidLoad 메소드는 뷰의 로딩이 완료 되었을 때 시스템에 의해 자동으로 호출된다 그렇기 때문에 일반적으로 리소스를 초기화하거나 초기 화면을 구성하는 용도로 주로 사용된다
아까 전에도 말했듯이 화면이 처음 만들어질 때 한 번만 실행되므로, 처음 한 번만 실행해야 하는 초기화 코드가 있을 경우 이 메소드 내부에 작성하면 된다

```
 override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    }
```

viewWillAppear이라는 메소드를 오버라이드 했는데 viewWillAppear는 어떤 메소드 일까?? 바로 ViewController의 생명 주기에 관련된 메소드이다
**viewWillAppear은 뷰가 이제 나타날 거라는 신호를 컨트롤러에게 알리는 역활을 한다**
즉, 뷰가 나타나기 바로 직전에 호출된다고 볼 수 있다

viewWillAppear을 알아봤으니 저 메소드는 언제 쓰고 뭐할때 사용할까? 저 안에는 무엇을 넣어야 할까? 바로 뷰가 나타나기 바로 직전에 해야할 것들을 정의해주는 코드를 작성한다

그리고 파라미터로 되어있는 animatedL: Bool 은 quick help를 살펴보면 true일 경우, 애니메이션을 이용하여 뷰가 윈도우에 얹혀진다.

```
 override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    
    viewControllers = [
      TableViewBasic(),
      TableViewLifeCycle(),
      TableViewSection(),
      TableViewRefresh(),
      TableViewCellStyle(),
      TableViewCustomCell(),
      TableViewEditing(),
    ]
  }
}
```

이번에는 viewWillAppear 안에 있는 코드를 살펴 보자

위에서 먼저 말햇던 viewControllers는 UIViewController 클래스 자료형을 타입을 받아 Array로 하여 받은 빈 배열인데, 즉 UIViewController 클래스는 모두 배열 안에 값으로 받을 수 있다

그래서 그 안에 UIViewController의 여러 인스턴스들이 배열 값으로 들어가 있다

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

위의 코드는 UITableDataSource에 대한 코드이다

한번 천천히 뜯어 보자.

먼저 ListViewController을 **extension**을 사용하여 확장시켰다, 그래서 ListViewController은 UITableViewDataSource는 프로토콜인데 이 프로토콜을 채택하겠다는 뜻이다 그런데 지금은 안보이지만 첨부한 전체 코드를 열어서 보면 **tableView.dataSource = self** 와 같은 코드가 없는데 처럼 UITableDataSource 프로토콜을 채택한것과 동일한 실행을 한다 어떻게 된것일까??

![img](https://user-images.githubusercontent.com/42841888/56036323-912a6480-5d67-11e9-9592-e5e98404b505.png)

바로 스토리보드 상에서 위의 그림과 같이 테이블 뷰를 끌어서 리스트 뷰 컨트롤러와 연결하여 dataSource와 delegate를 연결해 주었기 때문에

```
tableView.dataSource = self
tableView.delegate = self
```

위와 같은 코드를 안써줘도 된다

다시 뜯어보면,

UITableViewDataSource 프로토콜을 채택한 ListViewController 확장내에 있는 메소드를 보면

```
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return viewControllers.count
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
  }
```

이런데 먼저

```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return viewControllers.count
  }
```

를 봐보면 quick help에는 **테이블 뷰에 지정된 섹션에있는 행의 수를 반환하도록 데이터 소스에 지시 합니다**라고 나와있다
파라미터로 나와있는 tableView는 이 정보를 요청하는 테이블 뷰 객체를 받고, section은 테이블 뷰의 섹션을 식별하는 인덱스 번호를 받는다
그래서 리턴값으로 return viewControllers.count, 그 이유는 viewControllers Array에 들어있는 TableViewBasic(), TableViewLifeCycle(), TableViewSection(), TableViewRefresh(), TableViewCellStyle(), TableViewCustomCell(), TableViewEditing() 의 갯수만큼 받아야 하기 때문에
즉, 7개의 행의 수를 반환하여야 하기 때무에 viewControllers.count를 리턴값으로 했다

그리고 다음 메소드를 보면,

```
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
```

이 메소드는 **테이블 뷰의 특정 위치에 삽입 할 셀의 데이터 소스를 요구합니다**라고 나와있다 이 역시도 quick help를 보면 나온다
파라미터로 나와있는 tableView 는 셀을 요청하는 테이블 뷰 객체를 받고, indexPath는 테이블 뷰에서 행을 찾는 index 경로를 받는다

반환값으로 UITableViewCell 타입을 반환받는데 상수 cell을 먼저 만들어 그 안에 UITable 의 메소드인 dequeueReusableCell를 사용하는데
dequeueReusableCell는 **지정된 재사용 ID에 대한 재사용 가능한 테이블 뷰 셀 객체를 반환하고 이를 테이블에 추가한다**고 나와있다
dequeueReusableCell의 파라미터인 withIdentifier는 **재사용 할 셀 객체를 식별하는 문자열이다 즉, ID이다, 이 매개변수(parameter)는 nil이 아니여야 한다**
indexPath 파라미터는 **셀의 위치를 지정하는 인덱스 경로이다, 항상 데이터 소스 객체에서 제공하는 인덱스 경로를 지정하여야 한다, 이 방법은 인덱스 경로를 사용하여 테이블 뷰에서 셀의 위치를 기반으로 추가 구성** 한다고 나와 있다

다음으로는

```
extension ListViewController: UITableViewDelegate {
  func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let vc = viewControllers[indexPath.row]
    navigationController?.pushViewController(vc, animated: true)
  }
}
```

를 보자 UITableDelegate는 선택사항을 관리하고, headers와 footers 섹션의 구성, 셀의 삭제 및 순서의 재구성 그리고 테이블 뷰에서 다른 액션 수행 방법을 구상한 프로토콜이다.
조금 더 상세히 말해보면 다음과 같은 기능 을 관리할 수 있다.
사용자 정의의 headers와 footers의 작성 및 관리, headers와 footers에 대한 행의 높이를 지정할 수 있으며, 더 나은 scrolling을 위한 높이 예상치 제공, 행의 내용을 들여쓰거나 행의 선택에 응답하는 것, swipes 및 테이블 뷰의 다른 액션에 응답하고, 테이블 내용의 수정을 지원한다

UITableDelegate 프로토콜의 메소드 중 optional func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) 을 구현했는데 이 메소드는 지정된 행이 선택되었다고 델리게이트에게(대리자) 알리는 메소드 이다
이 메소드의 파라미터인 tableView는 새로운 행 선택에 대해 델리게이트에게 알리는 테이블 뷰 객체를 받고, indexPath는 테이블 뷰에서 새롭게 선택된 행을 찾는 인덱스 경로를 받는다

그런데 위에서부터 계속 인덱스 경로 또는 indexPath에 대해 나오는데 이것을 quick help에서 보면 **중첩 배열 트리의 특정 위치에 대한 경로를 함께 나타내는 인덱스 목록** 이라고 나와있다

```
let vc = viewControllers[indexPath.row]
```

상수 vc는 viewControllers의 인덱스 경로의 행 요소의 값을 vc에 넣어주는 코드

```
navigationController?.pushViewController(vc, animated: true)
```

navigationController?는 **뷰 컨트롤러 계층에서 가장 가까운 네비게이션 컨트롤러의 조상이라고 나오고,**
UINavigationController의 메소드 pushViewController는 **뷰 컨트롤러를 receiver의 스택에 푸시하고 디스플레이를 업데이트 한다**

pushViewController의 파라미터인 viewController는 
**스택에 푸시된 뷰 컨트롤러를 받는다, 이 객체는 탭 바 컨트롤러가 될 수 없고, 만약에 뷰 컨트롤러가 이미 네비게이션 스택에 있는 경우에는 이 메소드는 exception을 던진다**
pushViewController의 다른 파라미터인 animated는 **화면 효과를 나타나게 하려면 true, 아니면 false를 지정하면 된다, 그리고 실행시(launch time) 네비게이션 컨트롤러를 설정하려면 false를 지정**

그래서 

```
let vc = viewControllers[indexPath.row]
navigationController?.pushViewController(vc, animated: true)
```

스택에 푸시된 viewControllers 안에 있는 뷰 컨트롤러의 row 에 따라 하나씩 접근하여 빼내는 코드인 **viewControllers[indexPath.row]** 이것을
vc에 주고, pushViewController 메소드의 파라미터인 viewController를 vc로 받고, animated는 true로 주었다
그래서 vc에 값에 따른 뷰 컨트롤러를 화면에 띄워준다, 네비게이션 컨트롤러를 이용하여.
