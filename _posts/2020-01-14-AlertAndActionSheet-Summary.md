---
layout: post
title:  "Alert And ActionSheet Summary"
date:   2020-01-14
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - Alert And ActionSheet](https://www.edwith.org/boostcourse-ios/lecture/16864/)

- - -

### Alert  And ActionSheet

- 사용자에게 경고 또는 알림 메시지를 표시하기 위한 얼럿과 액션시트

- - -

![AlertAndActionSheetImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AlertAndActionSheetImage-1.png?raw=true)

![AlertAndActionSheetImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AlertAndActionSheetImage-2.png?raw=true)

- - -

### UIAlertController 클래스

- UIAlertController 클래스는 사용자에게 표시할 얼럿 또는 액션시트 구성에 관한 메서드와 프로퍼티를 포함하고 있다

- UIAlertController 클래스를 통해 얼럿 또는 액션시트를 구성한 후 UIViewController의 present(_:animated:completion:) 메서드를 사용하여 사용자에게 얼럿 또는 액션시트를 Modal로 보여준다

- - -

### UIAlertController의 주요 메서드

- init(title:message:preferredStyle:)

    - 얼럿 뷰 컨트롤러의 객체를 초기화
    
- func addAction(UIAlertAction)
    
    - 얼럿이나 액션시트에 액션을 추가
    
- func addTextFiedl(configurationHandler: ((UITextField) -> Void)? = nil)

    - 얼럿을 통해 텍스트를 입력받고자 하는 경우 텍스트 필드를 추가
    
- - -

### UIAlertController의 주요 프로퍼티

- var title: String?
    
    - 얼럿의 제목
    
- var message: String?
    
    - 얼럿에 대해 좀 더 자세히 설명하는 텍스트
    
- var actions: [UIAlertAction]
    
    - 사용자가 얼럿 또는 액션시트에 응답하여 실행할 수 있는 액션
    
- var preferredStyle: UIAlertController.Style

    - 얼럿 컨트롤러의 스타일, 얼럿과 액션시트가 있다
    
- - -

### UIAlertAction 클래스

- 사용자가 얼럿 또는 액션시트에서 사용할 버튼과 버튼을 탭 했을 때 수행할 액션을 구성할 수 있다

- UIAlertAction 클래스를 사용하여 버튼을 구성한 후 UIAlertController 객체에 추가하여 사용한다

- - -

### UIAlertAction의 주요 프로퍼티

- var title: String? 

    - 액션 버튼의 타이틀
    
- var isEnabled: Bool

    - 액션이 현재 사용 가능한지를 나타낸다
    
- var style: UIAlertAction.Style

    - 액션 버튼의 적용될 스타일
    
- - -

### UIAlertAction.Style

- default
    
    - 액션 버튼의 기본 스타일
    
- cancle
    
    - 액션 작업을 취소하거나 상태 유지를 위해 변경사항이 없을 경우 적용하는 스타일
    
- destructive

    - 취하게 될 액션이 데이터를 변경되거나 삭제하여 돌이킬 수 없는 상황이 될 수 있음을 나타낼 때 사용하는 스타일
    
![UIAlertActionStyleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIAlertActionStyleImage-1.png?raw=true)

![UIAlertActionStyleImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIAlertActionStyleImage-2.png?raw=true)

- - -

### When I used Alert and ActionSheet ?

- the time is now to used Alert !!

    - 중요한 액션을 하기 전 경고가 필요한 경우

    - 액션을 취소할 기회를 제공해야 하는 경우

    - 사용자의 작업을 한 번 더 확인하거나 삭제 등의 작업을 수행하거나 문제 사항을 알릴 때

    - 결정이 필요한 중요 정보를 표시할 경우

- the time is now to used ActionSheet !!

    - 사용자가 고를 수 있는 액션 목록이 여러 개일 경우
    
    - 새 작업 창을 열거나, 종료 여부 확인 시
    
    - 사용자의 결정을 되돌리거나 그 동작이 중요하지 않을 경우

- - -