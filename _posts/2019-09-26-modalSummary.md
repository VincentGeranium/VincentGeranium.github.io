---
layout: post
title:  "모달 구현해보기 정리"
date:   2019-09-26
categories: iOS, Swift
---

이 포스트는 edwith의 부스트코스 iOS 프로그래밍을 듣고 정리한 내용입니다

- - -

### 모달 구현해보기

- - -

- 스토리보드 상으로 새로운 뷰 컨트롤러 2개를 만든 뒤 initial View Controller로 첫 번째 뷰 컨트롤러를 시작점으로 만들어 주었다.

- 첫 번째 뷰 컨트롤러에 `Present Modal`이라는 버튼을 만들어 두 번째 뷰 컨트롤러로 넘어가게 연결해주었는데 그때 `Present Modally`로 연결해주었다.

- 두 번째 뷰 컨트롤러는 `SecondViewController.swift` 파일과 연결해 주었다.

![initModalStoryboard](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/initModalStoryboard.png?raw=true)

- 두 번째 뷰 컨트롤러에는 `dismiss Modal`이라는 버튼을 만들고 `SecondViewController.swift` 파일 내에 `@IBAction func didTappedDismissBtn()` 메소드를 만들어 두 번째 뷰를 `dismiss` 할수 있도록 만들어 주었다.

![secondVCbtnAction](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/secondVCbtnAction.png?raw=true)

- - -

### 내비게이션과 모달의 차이

- 내비게이션 인터페이스에서 다음 화면으로 넘어가는 것은 **PUSH**, 이전 화면으로 가는 것은 **POP**

- 모달에서 올려주는 것은 **Present**, 사라지는 것은 **Dismiss**

- **서로의 쌍이 다르다**

- **내비게이션과 모달의 용도는 굉장히 다르다**

    - 내비게이션 인터페이스 같은 경우 **정보의 흐름이 연결될 때 사용**
    
        - 예를 들어 설정 화면, 설정화면은 일정한 정보의 흐름을 가지고 이동한다
        
        - 설정 -> 일반 이러한 정보의 흐름
        
        ![setting_1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/setting_1.PNG?raw=true)![setting_2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/setting_2.PNG?raw=true)
        
- 모달은 **단순한 팝업, 사용자의 주의를 끌기 위함, 장시간의 입력 폼**등을 위한 팝업

    - 예를 들어 메시지 앱 같은 경우 메시지에 들어와서 사람의 이름을 누르면 그 사람과 한 내용의 메시지로 들어오게 된다 이러한 것은 정보의 흐름이 있어 내비게이션 인터페이스로 구현되어 있고
    
    - 이 안에 들어와 인포 버튼을 누르면 그 사람의 인포를 확인하기 위해 모달이 올라온다
    
        - 잠깐 이 사람에 대한 간략한 정보를 보여주고 넘어갈 용도 이므로 모달로 구현
        
        ![message_1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/message_1.PNG?raw=true)![message_2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/message_2.PNG?raw=true)
        
- **만약 용도와 다르게 내비게이션 인터페이스나 모달을 잘못 사용하면 사용자게엑 큰 불편함으로 작용할 수 있다.**

- **그래서 화면 전환을 어떻게 제대로 해줄 것인가에 대한 고민을 많이 해보고 H.I.G 에 맞춰 디자인해야 한다.**