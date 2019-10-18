---
layout: post
title:  "Target Action Design Pattern 활용"
date:   2019-10-18
categories: iOS, Swift
---

이 포스트는 edwith의 부스트코스 iOS 프로그래밍을 보고 공부한 후 정리한 내용입니다

[edwith iOS 프로그래밍 - ㅅTarget Action Design Pattern 활용](https://www.edwith.org/boostcourse-ios/lecture/16885/)

---

### Target Action 디자인패턴을 활용하여 UIDatePicker 사용

- - -

### UIDatePicker

- Date Picker은 날짜 및 시간을 입력하는 컨트롤이다.

- Date Picker을 이용하여 특정 시점의 날짜와 시간 또는 시간 간격을 입력 할 수 있다

![UIDatePickerImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIDatePickerImage-1.png?raw=true)

- - -

### Date Picker을 인테페이스에 추가하기

- Date Picker을 생성하고 모드를 설정한다

- 필요한 경우 최소 및 최대 날짜와 같은 추가 구성 옵션을 제공한다

- Date Picker에 액션 메서드를 연결한다

- - -

### Date Picker에 액션 메서드 연결하기

- Date Picker은 사용자가 선택된 날짜를 바꿀 경우 애플리케이션에 알리기 위해 타겟 액션 디자인 패턴을 사용한다

- Date Picker의 값이 변경될 때 알림을 받기 위해 액션 메서드를 valueChanged로 설정한다

- 실행시점에서 Date Picker는 사용자의 날짜 및 시간을 선택하게 되면 설정된 액션 메서드를 호출한다

- Date Picker를 액션 메서드에 연결하기 위해 인터페이스 빌더를 시용하거나 코드로 addTarget(_:action:for:)메서드를 사용한다

- - -

### Date Picker의 주요 인터페이스 빌더 속성

![UIDatePickerImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UIDatePickerImage-2.png?raw=true)

- Mode

    - Date Picker의 모드를 설정한다.

    - 코드상으로 datePickerMode 프로퍼티를 사용하여 이 값에 접근할 수 있다
    
- Locale

    - Date Picker에 사용될 locale(로케일은 사용자의 언어, 국가뿐 아니라 사용자 인터페이스에서 사용자가 선호하는 사항을 지정한 매개 변수의 모임이다)

    - 코드상으로 locale 프로퍼티를 통해 이 값에 접근할 수 있다
    
- Interval
    
    - 현재 선택된 모드의 분 간격을 나타낸다. 선택한 값은 60의 제수여야한다.

    - 코드상으로 minnuteInterval 프로퍼티를 통해 이 값에 접근할 수 있다
    
- Constraints
    
    - Date 하단의 Minimum Date와 Maximum Date를 통해 Date Picker가 보여줄 날짜의 범위를 설정할 수 있다

    - 코드상으로 minimumDate, maximumDate 프로퍼티를 통해 설정할 수 있다.
    
- Timer
    
    - 카운트다운 타이머 모드에서 date picker의 표시되는 초기값이다. 값은 초 단위로 계산되지만 보이는 것은 분 단위로 표시된다

    - 코드상으로 countDownDuration 프로퍼티를 통해 이 값에 접근할 수 있다.
    
- - -

### UIDatePicker 클래스의 주요 프로퍼티

- var datePickerMode: UIDatePickerMode
    
    - Date Picker의 모드를 결정한다
    
    - 기본값은 dateAndTime이다
    
    - time, date, dateAndTime, countDownTimer 네가지 모드를 설정할 수 있다
    
- var date: Date

    - Date Picekr에 보여지게 될 날짜
    
- var calendar: Calendar!

    - Date Picker에 사용되는 캘린더이다
    
- var locale: Locale?

    - Date Picker에서 사용하는 로케일이다
    
- var timeZone: TimeZone?
    
    - Date Picker에서 표시된 날짜에 반영된 시간대이다
    
- var maximumDate: Date?

    - Date Picker에서 보여줄 수 있는 최대 날짜이다
    
- var minimumDate: Date?

    - Date Picker에서 보여줄 수 있는 최소 날짜이다
    
- minuteInterval: Int

    - Date Picker에서 분을 표시하는 간격이다. 기본값과 최솟값은 1이고 최대값은 30이다
    
- var countDownDuration: TimeInterval

    - Date Picker의 모드가 countDownTimer로 설정될 경우 Date Picker에 표시되는 초깃값이다
    
- - -

### UIDatePicker 클래스의 주요 메서드

- func setDate(Date, animated: Bool)

    - Date Picker에 처음 표시할 날짜를 설정한다
    
- - -

### DateFormatter

- **DateFormatter는 날짜와 텍스트 표현 간의 변환을 할 수 있게 해준다**

- DateFormatter를 활용해 날짜와 시간을 다양한 방식으로 출력하거나 출력된 날짜 및 시간에 대한 문자열을 읽어올 수 있다

- **DateFormatter의 인스턴스는 Date 객체의 문자열 표현을 생성하고, 날짜 및 시간의 텍스트 표현을 Date 객체로 변환한다**

[Apple Documentation - Date](https://developer.apple.com/documentation/foundation/date)

- - -

### 사용자 날짜 및 시간 표현

- 사용자에게 날짜를 표시할 때 특정 요구 사항에 따라 date formatter의 dateStyle과 timeStyle 프로퍼티를 설정한다

    - 예를들어, 만약 시간을 제외한 월, 일, 연도를 보여주고 싶다면, dateStyle 프로퍼티를 long로 설정하고 timeStyle를 none으로 설정한다
    
    - 시간만 보여주고 싶다면 dateStyle 프로퍼티를 none로 timeStyle 프로퍼티를 short로 설정한다
    
    - dateStyle와 timeStyle 프로퍼티의 값을 기반으로 DateFormatter는 지정된 로케일에 적합한 지전된 날짜의 표현을 제공한다
    
    - 미리 정의된 스타일을 통해 얻을 수 없는 형식을 지정해야 한다면 setLocalizedDateFormatFromTemplate(_:)을 사용하여 날짜 형식을 지정할 수 있다
    
- - -

### 고정 형식 날짜 표현

- RFC3339와 같은 고정 형식의 날짜로 사용해야 한다면, dateFormat 프로퍼티를 특정 문자열로 설정한다

- 대부분의 경우 고정된 형식의 경우 locale 프로퍼티를 POSIX locale("en_US_POSIX")로 설정하고, timeZone 프로퍼티를 UTC로 설정한다

- - -

### DateFormatter의 주요 프로퍼티와 메서드

- func date(from: String)

    - 주어진 문자열을 Date 객체(날짜와 시간)로 변환하여 반환한다
    
- func string(from: Date)

    - 주어진 Date 객체를 문자열로 변환하여 반환한다
    
- func setLocalizedDateFormatFromTemplate(String)

    - 지정된 로케일을 사용하여 날짜 형식을 설정한다
    
- var dateStyle: DateFormatter.Style

    - DateFormatter의 날짜 형식
    
- var timeStyle: DateFormatter.Style

    - DateFormatter의 시간 형식
    
- var locale: Locale!

    - DateFormatter의 로케일 이다
    
- var timeZone: TimeZone!

    - DateFormatter의 시간대이다
    