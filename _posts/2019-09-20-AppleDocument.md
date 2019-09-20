---
layout: post
title:  "애플 개발자 문서 읽기"
date:   2019-09-20
categories: iOS, Swift
---

이 포스트는 edwith의 부스트코스 iOS 프로그래밍을 학습한 뒤 정리한 내용입니다.

- - -

### 애플 개발자 문서

- 애플에서 제공하는 개발 문서에 익숙해져야 한다.

- 문서에서 필요한 정보를 습득하는 일은 iOS 개발에 있어 매우 중요하다.

- 문서를 숙지해 프레임워크와 클래스의 구동 방식을 이해하고 적절한 메서드와 프로퍼티를 찾아 애플리케이션에 올바르게 적용할 수 있다.

- 오류가 발생했을 때 적절한 해결방안을 찾을 수 있다.

- 새롭게 등장하는 기술을 빠르게 이해하고 응용할 수 있다

- - -

### 애플 개발자 문서의 구성

**애플 개방 사이트의 문서는 크게 3가지로 나누어져 있다.**

- - -

![API-Reference-Image](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/APIReference.png?raw=true)

- 1. 참조 자료(API Reference)

    - 클래스의 메서드와 프로퍼티에 대한 기술적인 세부사항에 관해 설명한다.
    
    - 코딩을 계획하거나 코딩을 하는 중에 살펴보는 말 그대로 참조용 자료.
    
![Guide-Image](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/Guide.png?raw=true)
    
- 2. 가이드(Guide)

    - 가이드는 특정 분야에 대해 상세히 소개
    
    - 내부적으로 어떻게 구동되는지에 대해 설명
    
    - 관심 있는 부분만 골라서 읽어도 되지만, 모든 부분을 읽으면 예상치 못한 정보를 많이 배우게 될 것이다.
    
    - 짤막한 예제코드를 제공하는 경우도 있기 때문에 올바른 코딩에 많은 도움이 된다.
    
![Sample-Code-Image](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/SampleCode.png?raw=true)

- 3. 샘플 코드(Sample Code)

    - 샘플 코드 실제로 API를 어떻게 사용하는지에 대한 예시
    
    - 동일한 기능을 애플의 프로그래머는 어떻게 구현하는지, 어떻게 코드를 작성하는지 살펴볼 수 있다.
    
- - -

### 애플 문서 읽기 팁

- 먼저 사용하려는 클래스의 가이드를 읽어 개략적인 기능에 대해 이해하는것이 좋다

    - 그런 다음 참조 자료를 살펴보면서 애플리케이션에 구현할 기능(Property)이나 작동방법(Method)을 숙지하는 것이 좋다
    
- - -

### 애플 문서 읽기 예시

- UITextField를 사용하는 경우

    - 1. Text Programming Guide for iOS 가이드 문서의 개요를 통해 UIKit 중 문자를 보여주거나 관리하는 주요 구서요소와 기능에 대해 살펴본다
    
        - UITextField 외에 문자를 다루는 다른 클래스(UITextLable, UITextView)에는 무엇이 있는지도 함께 살펴보고 차이에 대해 이해하면 좋다.
        
    - 2. UITextField 참조 문서를 통해 기본적인 객체를 어떻게 생성할 수 있는지 알아본다.
    
    - 3. 텍스트 필드의 문자 색상/폰트/정렬 방법을 수정하고 싶다면 프로퍼티 부분을 살펴본다
    
    - 4. 텍스트 필스의 모양과 위치를 재정의하고 싶으면 메서드 부분을 살펴본다
    
    - 5. 만약 원하는 프로퍼티나 메서드를 찾을 수 없다면 부모클래스의 문서로 이동하여 원하는 기능을 찾아본다
    
    - 6. 텍스트 필드에 특정 이벤트가 발생하는 것을 감지하고 싶다면 델리게이트가 있는지 살펴본다
    
        - 델리게이트가 있다면 해당 프로토콜 문서를 찾아가 살펴본다
    
- 만약 OS 버전에 따라서 특정 동작을 하지 않거나 오류가 발생시 Deprecated 된 기능을 사용하고 있는지 확인해본다.

- - -

### 문서 접근 방법

- - -

##### 1. 애플 개발자 사이트에서 문서 보기

![AppleDocumentImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AppleDocumentationWeb.png?raw=true)

- - -

##### 2. Xcode Quick Help

![XcodeQuick](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/XcodeQuickHelp.png?raw=true)

- - -

##### 3. Xcode 메뉴 > Help > Developer Documentation

![XcodeHelpMenu](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/XcodeHelp.png?raw=true)

- - -

##### 4. Xcode 클래스 위 커서 + Option + 클릭

![XcodeOption](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/XcodeOption.png?raw=true)