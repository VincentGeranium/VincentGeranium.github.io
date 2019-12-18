---
layout: post
title:  "프로젝트 진행중에 배운 점 - Summary(2)"
date:   2019-12-19
categories: iOS, Swift
---

### UIModalPresentationStyle And View State (View Life Cycle)

edwith Project B(PJT-2)를 진행하면서 code review를 받은 부분 중 수정해야 할 과정이 있었는데

모든 회원가입 과정, 유저로부터의 데이터를 받아와 입력이 성공적으로 끝이나면 제일 첫 화면 (로그인 화면)으로

넘어가는데 첫 로그인 메인 화면에 ID textField에 유저가 성공적으로 가입을 한다면 id가 자동적으로 입력이

되어 보여주게 하는 것이다

- 회원가입 전, 후의 로그인 메인 화면

<img width="200" alt="beforeSignUp" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/beforeSignUp.png?raw=true"><img width="200" alt="afterSignUp" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/afterSignUp.png?raw=true">

이 프로젝트에서 유저의 정보를 넘겨주거나 저장은 Singleton Design Pattern으로 구성하여 진행하였다

두 번째 VC에서 유저의 ID 정보를 받아 UserInfomation(Singleton Design) 으로 저장하고 다른 뷰에 전달 할 수 있도록 하는데

두 번째 VC에서 받은 ID 정보를 성공적으로 회원가입에 성공했을때 첫 번째 VC의 ID textField에서 보여줘야 하니까

마지막 VC가 사라지면 첫 번째 VC의 viewWillAppear에서 UserInfomation의 ID 정보를 받아 보여주면 되겠다고 생각했다

그런데 여기서 문제가 생겼다

iOS 13에서 바뀐 modal presentation style 때문이였다

이 전에 포스팅 했던 [프로젝트 진행중에 배운 점 - Summary(1)](https://vincentgeranium.github.io/ios,/swift/2019/12/18/DuringProjects-Summary.html) 에서 보면 이 프로젝트는 첫 번째 VC에서 두 번째 VC로 넘어갈때 present 형식으로 화면을 전환했다

두 번째 VC에서 마지막 VC는 navigation push 방식으로 화면을 전환했지만 마지막 VC에서 첫 번째 VC로

화면이 전환될때는 dismiss 방식으로 화면을 내려줘야 했다

- 마지막 VC에서 성공적으로 회원가입이 되고 VC를 dismiss 해 주는 코드

```swift

    // MARK: - btnIsSelectedState()
    /// 가입버튼이 활성화 되었을 때 전화번호, 생년월일은 singleton으로 넘어가며 singleton에 저장되어 있던 id는 FirstViewController의 id 텍스트 필드의 텍스트로 할당해줌 그리고 이 뷰는 사라지게 만듦
    
    @objc private func btnIsSelectedState() {
        
        UserInfomation.shared.phoneNumber = phoneNumTextField.text
        UserInfomation.shared.dateOfBirth = dateOfBirthDisplay.text
        
        self.navigationController?.dismiss(animated: true, completion: nil)
        
        print("🔴🔴🔴🔴 : 가입버튼 정상 작동")
        
    }
    
```

그런데 이렇게 dismiss를 해주었을때 첫 번째 VC에서는 viewWillAppear 이 불리어지지 않았다

이게 문제가 되어 첫번째 VC의 View가 Load 되기 전에 첫번째 VC의 ID textField에 ID 데이터를 불리어줄수없게 되엇다

왜 그럴까 생각해보니 iOS 13의 presentStyle 때문이였다

기본적으로 modalPresentatingStyle를 iOS 13에서는 지정해주지 않으면 default 값으로 pageSheet으로 지정이 되어 

다른 VC를 Present했을때 첫번째 VC가 뷰의 계층에서 사라지지 않고 계속 살아있게 되있는것이다

그래서 dismiss를 해도 뷰의 라이프 사이클에서 viewWillAppear이 나타나지 않게 되는 것이다

그래서 UIModalPresentationStyle을 .fullScreen으로 바꾸어주어야 한다

- 첫 번째 VC에서 두 번째 VC로 화면을 전환하는 코드

```swift

    // MARK: - didTappedSignUpBtn
    /// Sign Up Button을 눌럿을때 동작
    @objc private func didTappedSignUpBtn(_ sender: UIButton) {
        
        let naviVC = UINavigationController(rootViewController: SignUpViewController())
        
        naviVC.modalPresentationStyle = .fullScreen
        
        self.present(naviVC, animated: true, completion: nil)
    }
    
```

Sign Up Button을 눌럿을때 naviVC.modalPresentationStyle = .fullScreen 으로 지정해주어

첫 번째 VC가 두 번째 VC로 화면이 전환되면서 뷰의 계층에서 사라지게 만들어주었고 

그러면서 마지막 VC에서 다시 첫 번째 VC로 화면을 전환(dismiss) 했을때 첫 번째 VC의 뷰 계층 viewWillAppear 계층이 나올수있도록 해주었다

그러면서 viewWillAppear 부분에 UserInfomation의 ID 정보를 받아와 첫번째 VC에서 받을수잇는 코드를 작성하여 첫 번째 VC ID textField에서 보여줄 수 있도록 만들어 문제를 해결하였다

- [PJT-2 Project repo](https://github.com/VincentGeranium/edwithStudy-project-3/tree/master/PJT2-SignUp)

- [공부 중 찾은 blog -> about UIModalPresentationStyle](https://zeddios.tistory.com/828)

