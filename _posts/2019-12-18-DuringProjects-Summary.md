---
layout: post
title:  "프로젝트 진행중에 배운 점 - Summary"
date:   2019-12-18
categories: iOS, Swift
---

### UINavigationController Embed Programmatically

edwith boostcourse iOS Programming Project B 회원가입 부분에서 첫 VC에서 두 번째 VC로 넘어갈때는 present modal을 이용해 화면을 전환하였다

그러나 문제는 두 번째 VC가 UINavigationController의 rootViewController이여야 했으며 그 뒤로 3번째 VC가 navigation을 이용하여 push와 pop을 이용하여 화면을 전환하여야 하는 방식이였다

그 당시에 첫 번째 VC에서 두 번째 VC로 present는 잘되었는데 두번째 VC를 어떻게 코드로 navigation의 rootVC로 만드는지가 가장 핵심 문제였다

아에 첫 VC가 navigation의 rootVC였다면 SceneDelegate에서 처음 window의 rootVC를 첫 VC를 navigation의 rootVC로 만들어 붙여줬다면 첫 VC부터 navigation의 rootVC가 되어 쉽게 진행되었을것이다

그러나 나는 중간에 navi의 rootVC로 만드는 방법에 무지하여 여러 방법을 시도하였고 그러던 중 다음과 같이 두 번째 VC를 navi의 rootVC로 만들 수 있었다

```swift

    // MARK: - didTappedSignUpBtn
    /// Sign Up Button을 눌럿을때 동작
    @objc private func didTappedSignUpBtn(_ sender: UIButton) {
        
        let naviVC = UINavigationController(rootViewController: SignUpViewController())
        
        naviVC.modalPresentationStyle = .fullScreen
        
        self.present(naviVC, animated: true, completion: nil)
    }

```

- SignUp 버튼을 누르면 두 번째 VC로 Present로 화면이 전환되는 코드

- 두 번째 VC(SignUpViewController)는 navigation의 rootVC로 지정하여 let naviVC로 인스턴스화

- 첫 번째 VC (self)로 present하는데 naviVC를 present

- [PJT-2 Project repo](https://github.com/VincentGeranium/edwithStudy-project-3/tree/master/PJT2-SignUp)

- [공부 중 찾은 blog -> about UINavigationController Embed Programmatically](https://anum.io/2018/02/15/embed-a-uiviewcontroller-in-a-uinavigationcontroller-programmatically/)

- - -

