# 나의, 나를 위한, 나에 의한 Delegate 이해하기!!

스위프트를 공부하면서 처음부터 끝까지 많은 것들이 이해가 안가지만 그 중에서도 왠지 난이도가 거의 슈퍼마리오 쿠퍼 느낌의 Delegate!!
이 Delegate에 대해서 나의, 나를 위한, 나에 의한 이해도 높이기 !!

먼저 Delegate를 알려면 그 전에 먼저 알아야 할 것이 있는데 그게 바로 Protocol 이다
왜 그럴까?? 바로 Delegate가 프로토콜로 구현되기 때문이다
그렇다면 프로토콜은 또 뭘까?? 일단 이 포스트는 Delegate를 이해하기 위한 포스트니까 프로토콜에 대해서는 이해하기 쉽게 빠른 예시로 마무리하고 나중에 다시 프로토콜에 대해서 알아보도록 하자

다시 본론으로 돌아와 프로토콜은 **그냥 서로간의 약속** 이라고 생각하면 편하다

예를들면 "과일"이라는 프로토콜이 있다고 상상해보자
과일 프로토콜은 공통적으로 맛을 내다(), 원산지, 품종, 성장 속도() 등등 여러가지를 가지고 있을것이다

과일 중 바나나, 사과가 있다고 생각해보자
이 바나나와 사과는 과일의 일종이다
그래서 바나나와 사과는 꼭 과일 프로토콜을 준수해야만 한다

이 바나나와 사과는 "과일"이라는 큰 카테고리 안에 들어가 있는 것이다.

프로토콜 상에서는 맛을 내다(),성장 속도() 라는 행동을 **정의만 하고 구현은 하지 않았다**
그 이유는 무엇일까??

**그 구현은 "과일"이라는 프로토콜을 채택한 곳에서 이루어진다**

스위프트를 만들어낸 애플도 모든 경우의 수를 생각해 구현하기 힘들기 때문이다.

프로그래머는 함수 프로토타입을 가지고 자신만의 원하는 방향으로 구현만 하면 된다

**꼭 기억해야 할 한기지!! 프로토콜은 서로간의 지켜야할 규칙, 규약, 약속!!** 이다

프로토콜에 대해 어느정도 이해가 갔으니 본격적으로 무시 무시한 끝판왕 delegate를 공부해보자

먼저 delegate가 도대체 뭘까? 궁굼해서 검색해보니 영어 사전에서 나오길

1. 대표자

2. 위임하다

3. (대표를)뽑다

라는 뜻이 있다

내가 iOS를 공부하면서 나 보다 먼저 공부하셨거나 아니면 블로그를 뒤져서 보면 delegate는 항상 무엇인가를 대리해준다 라는 뜻으로 쓰인다는 말이나 글믈 많이 봐왔다

그래서 Delegate는 대리자 라는 뜻으로 이해하면 될 것 같다

약간 현실에서 "네가 해야할 일을 내가 해서 줄게" 같은 느낌??

스위프트에서 기존의 버튼이나 텍스트 필드, 라벨 등의 객체들은 고유의 특징들이 있다
버튼을 누르면 동작, 텍스트 필드는 글자를 입력, 라벨은 글자 내용을 출력 등...

**델리게이트 패턴은 쉽게 말해서, 객체 지향 프로그래밍에서 하나의 객체가 모든 일을 처리하는 것이 아니라 처리 해야 할 일 중 일부를 다른 객체에 넘기는 것을 뜻 한다**

조금 이해는 가지만 그래도 조금 더 확실한 이해를 위해서 delegate 예제를 봐가면서 해보자

예제는 text field안에 글자를 쓰고 버튼을 누르면 라벨에 내가 쓴 글이 옮겨지는 예제이다

프로젝트를 만들고, 메인 스토리보드에 텍스트 필드, 버튼, 레이블 이 순으로 배치를 한다

그리고 뷰 컨트롤러 클래스 안에 IBOutlet 레이블, 텍스트 필드를 구현하고 IBAction func 버튼을 구현한다

IBAction 안에는 다음과 같이 코드를 넣는다

```
@IBAction func didTapButton(_ sender: Any) {
    printLabel.text = textField.text
}
```

위 코드는 "라벨에 텍스트를 현재 내가 쓴 Text Field안의 값으로 써주겠다"라는 뜻이다

그리고 실행을 시켜 텍스트 필드 안에 글을 쓰고 버튼을 누르면 라벨이 텍스트 필드에 있던 값으로 바뀌게 된다

그렇다면 delegate를 써서 만들어 보자

**먼저 delegate를 사용하려면 과정이 존재하는데 첫번째로 가장 먼저 해주어야 할 작업은 "채택작업" 이다**

```
class ViewController: UIViewController, UITextFieldDelgate{
    @IBOutlet weak var textField: UITextField!
    @IBOutlet weak var printLabel: UILabel!
    @IBAction func didTapButton(_ sender: Any) {
        printLabel.text = textField.text
    }
}
```

- 먼저 **UIViewController** 옆에 UITextFieldDelegate라고 **"채택 작업"** 을 한다
- **프로토콜을 "선언" 했다는 말은 잘못된 말이다**
- 위의 코드를 예로들어 설명하면 프로토콜은 여러 프로토콜 중 UITextFieldDelegate를 채택하겠다는 의미이다

```
@IBAction func didTapButton(_ sender: Any) {
    // printLable.text = textField.text
}
```

- 델리게이트를 채택하고 나서 위의 코드처럼 @IBAction안에 동작처리를 주석으로 만들어준다
    - 그러면 이제 버튼을 눌러도 아무 동작하지 않게 된다
- delegate를 쓰는데 두번째 과정은 **위임자를 정해주는 과정** 이다

```
override func viewDidLoad() {
    super.viewDidLoad()
    textField.delegate = self
}
```

- viewDidLoad() 함수에 **textField.delegate = self** 를 추가했다
    - 이 코드는 **위임자(대리자)가 누구인지 알려주는 과정**이라고 생각하면 된다
    - textField의 심부름을 누가 할래? 했을때 textField의 심부름은 내가 도맡아 할게 라는 의미라고 보면된다
- 그렇다면 여기에서 "내가 할게"에서 "내"는 누구일까??
    - 바로 이 클래스인 **ViewController**이다
- ViewController은 textField에게 "너가 시키는 모든 심부름을 내가 다 할꺼야, 너한테 이벤트가 발생하면 프로토콜에 따라 너에게 응답을 줄게" 라는 말을 건네는 것과 같다
- 마지막 과정인 **구현**을 해보자
- @IBAction을 통해 글을 옮겨주는 것을 **대신해주는 함수**를 선언해보자

```
func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    printLabel.text = textField.text
    return true
}
```

- 위의 코드에서 처음보는 함수가 나왔다
- **textFieldShouldReturn**은 UITextFieldDelegate 안에 정의되어있는 함수이다
- 이 동작을 "대신"해 줄 함수를 불러와 그 함수안에 우리가 하고싶은 일을 "구현"만 하면 된다
- 그냥 함수의 이름만 보고 느껴지는 것은 텍스트 필드에 사용자가 어떤 일을 하고 리턴 될것이다 라는 의미같다
- 위에서 @IBAction 버튼 함수에서 사용했던 printLabel.text = textField.text를 추가하면 리턴 될 때 이 함수는 자동으로 불려오게 된다
- **실행을 해보면 버튼을 눌러봐도 안된다** 그러나 **버튼을 누르는 것이 아니고 엔터(enter)를 누르게 되면 텍스트 필드에 있던 내용이 라벨로 옮겨지게 된다**