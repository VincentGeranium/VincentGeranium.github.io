---
layout: post
title:  "Navigation Controller란?"
date:   2019-09-23
categories: iOS, Swift
---

이 포스트는 부스트코스의 iOS 강의를 학습 후 정리한 내용입니다

- - -

### UINavigation Controller 클래스

- **내비게이션 컨트롤러의 생성**

    - 내비게이션 컨트롤러의 인스턴스를 생성하는 메서드
    
    - 매개변수로 내비게이션 스택의 가장 아래에 있는 루트 뷰 컨트롤러가 될 뷰 컨트롤러를 넘겨준다

```swift
init(rootViewController: UIViewController)
```

- **내비게이션 스택의 뷰 컨트롤러에 대한 접근**

    - var topViewController = 내비게이션 스택에 있는 최상위 뷰 컨트롤러에 접근하기 위한 프로퍼티

    - var visibleViewController = 현재 내비게이션 인터페이스에서 보이는 뷰와 관련된 뷰 컨트롤러에 접근하기 위한 프로퍼티

    - var viewController = 내비게이션 스택에 특정 뷰 컨트롤러에 접근하기 위한 프로퍼티, 루트 뷰 컨트롤러의 인덱스는 0 이다.

```swift
var topViewController: UIViewController?

var visibleViewController: UIViewController?

var viewController: [UIViewContorller]
```

- **내비게이션 스택의 푸시(push)와 팝(pop)에 관한 메서드**

    - func pushViewController(UIViewController, animated: Bool)
        
        - 내비게이션 스택에 뷰 컨트롤러를 푸시(push)한다
        
        - 푸시 된 뷰 컨트롤러는 최상위 뷰 컨트롤러로 화면에 표시된다
        
    - func popViewController(animated: Bool) -> UIViewController?
    
        - 내비게이션 스택에 있는 최상위 뷰 컨트롤러를 팝(pop)한다
        
        - 최상위 뷰 컨트롤러 아래에 있던 뷰 컨트롤러 아래에 있던 뷰 컨트롤러의 콘텐츠가 화면에 표시된다
        
    - func popToRootViewController(animated: Bool) -> [UIViewController]?
    
        - 내비게이션 스택에서 루트 뷰 컨트롤러를 제외한 모든 뷰 컨트롤러를 팝(pop)한다
        
        - 루트 뷰 컨트롤러가 최상위  뷰 컨트롤러가 된다
        
        - 삭제된 모든 뷰 컨트롤러의 배열이 반환된다
        
    - func popToViewController(_ viewController: UIViewController, animated: Bool) -> [UIViewController]?
    
        - 특정 뷰 컨트롤러가 내비게이션 스택에 최상위 뷰 컨트롤러가 되기 전까지 상위에 있는 뷰 컨트롤러들을 팝(pop)한다

```swift
func pushViewController(UIViewController, animated: Bool)

func popViewController(animated: Bool) -> UIViewController?

func popToRootViewController(animated: Bool) -> [UIViewController]?

func popToViewController(_ viewController: UIViewController, animated: Bool) -> [UIViewController]?
```

- - -

### 내비게이션 인터페이스를 구성하는 두 가지 방법

- **[1] 스토리보드를 사용하여 내비게이션 인터페이스 구성하기**

    - 1) 스토리보드에서 내비게이션 컨트롤러에 포함할 뷰 컨트롤러를 선택한다
    
    - 2) 메뉴에서 [Editor] - [Embed In] - [Navigation Controller]를 차례로 선택한다
    
    - 3) 선택한 뷰 컨트롤러가 내비게이션 컨트롤러의 루트 뷰 컨트롤러가 되면서 내비게이션 컨트롤러가 생성된다
    
    - 위 방법 외에도 객체 라이브러리에서 내비게이션 컨트롤러를 드래그 엔 드랍 해서 캔버스에 올릴 경우 테이블 뷰를 포함한 루트 뷰 컨트롤러가 생성되면서 내비게이션 컨트롤러가 만들어진다.
    
- **[2] 코드작성을 통해 내비게이션 인터페이스 구성하기**

    - 코드로 내비게이션 컨트롤러를 생성할 경우, 내비게이션 컨트롤러가 생성되기 원하는 적절한 지검에 내비게이션 컨트롤러를 생성할 수 있다
    
        - 예를 들어 내비게이션 컨트롤러가 애플리케이션 윈도우(Window)의 루트 뷰로서 역활을 한다면, 내비게이션 컨트롤러를 applicationDidFinishLaunching: 메서드에 구현할 수 있다.
        
    - 1) 루트 뷰 컨트롤러가 될 뷰 컨트롤러를 생성한다, 이 객체는 처음에 내비게이션 스택의 최상위 뷰 컨트롤러가 화면에 보이게 되고 내비게이션 바에 뒤로가기 버튼이 생성되지 않는다.
    
    - 2) init(rootViewController: UIViewController) 메서드를 통해 내비게이션 컨트롤러를 초기화하고 생성한다
    
    - 3) 내비게이션 컨트롤러를 윈도우의 루트 뷰 컨트롤러로 설정한다
    
```swift
func application(_ appication: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

    // Override point for customization after application launch.
    
    // 루트 뷰 컨트롤러가 될 뷰 컨트롤러를 생성
    let rootViewController = UIViewController()
    
    // 위에서 생성한 뷰 컨트롤러로 내비게이션 컨트롤러를 생성
    let navigationController = UINavigationController(rootViewController: rootViewController)
    
    self.window = UIWindow(frame: UIScreen.main.bounds)
    
    // 윈도우의 루트 뷰 컨트롤러로 내비게이션 컨트롤러를 설정한다
    self.window?.rootViewController = navigationController
    self.window?.makeKeyAndVisible()
    
    return true
}
```

- - -

### 내비게이션 바의 구성

- 내비게이션 바는 내비게이션 컨트롤러에 의해 생성된다

- 내비게이션 바는 내비게이션 컨트롤러의 관리를 받는 모든 뷰 컨트롤러의 상단에 표시된다

- 최상위 뷰 컨트롤러가 변경될 때마다 내비게이션 컨츠롤러는 내비게이션 바를 업데이트 한다.

![navigationBar_1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/navigationBar_1.png?raw=true)

- 내비게이션 바는 다음과 같은 구조로 이루어져 있다

    - 내비게이션 바는 내비게이션 인터페이스에서 상단에 표시된다
    
    - 내비게이션 바는 내비게이션 아이템을 가질 수 있다
    
    - 뷰 컨트롤러가 전환될 때마다 내비게이션 바의 컨텐츠들이(내비게이션 아이템) 바뀌지만 내비게이션 바 자체는 내비게이션 컨트롤러가 관리하는 하나의 공통 객체이다
    
    - 내비게이션 바의 타이틀을 통해 현재의 위치(최상위 뷰 컨트롤러)를 알 수 있다.

![navigationBar_2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/navigationBar_2.png?raw=true)