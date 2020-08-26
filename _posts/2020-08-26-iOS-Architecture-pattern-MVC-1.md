---
layout: post
title:  "iOS Architecture pattern - MVC"
date:   2020-08-26
categories: iOS, Swift
---

이 포스트는 'Felipe Laso-Marsetti'의 'Model-View-Controller (MVC) in iOS – A Modern Approach' 내용을 정리한 포스트 입니다.

- - -
- - -

#### 참고 자료

[Model-View-Controller (MVC) in iOS – A Modern Approach](https://www.raywenderlich.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach)

- - -

### MVC 란?

MVC는 다음과 같은 세 가지 주요 객체로 구성된 소프트웨어 개발 패턴이다.

- **Model**은 데이터가 있는 곳이다. 지속성이 있는 데이터, 모델 객체, parsers, manager 그리고 네트워킹 코드 같은 것들이 **Model**에 들어있다.

- **View** 계층은 앱의 얼굴이다. 이것의 클래스는 도메인 로직을 포함하지 않기 때문에 종종 재사용될 수 있다. 예를 들어, 'UILabel'은 화면에 텍스트를 표시하는 뷰로, 재사용이 가능하고 확장이 가능하다.

- **Controller**은 Delegation pattern을 통해 뷰와 모델을 중재한다. 이상적인 시나리오는, 'Controller'는 자신이 다루고 있는 'View'를 모른다. 대신에, 프로토콜을 통하여 의사소통 할 것이다. 대표적인 예로 'UITableView'가 'UITableViewDataSource' 프로토콜을 통해 data source와 통신하는 방법이 있다.

<img alt="MVC-pattern" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/MVC-pattern.png?raw=true" title="MVC-pattern">

- 각각의 객체들은 다른 객체들과 분리되도록 되어 있고, 각각의 객체는 특정한 역활을 수행한다.

- [Apple’s MVC documentation](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Model-View-Controller/Model-View-Controller.html)은 MVC 계층을 상세히 설명하여 이론적인 이해를 제공한다. 그러나 실제적인 관점에서 보면 MVC 계층에 대한 설명이 부족하다.

- - -

### 각 계층에 대하여.

- - -

### The Model (M)

'Model' 계층은 앱의 모든 데이터를 포괄한다. 프로젝트에는 일반적으로 'Model' 계층에 포함할 수 있는 다른 클래스및 객체가 있다.

- **Network code** : 앱 전체에 걸친 네트워크 통신에는 단일 클래스만 사용하는 것이 좋다. HTTP 헤더 및 응답, 오류 처리 등 모든 네트워킹 요청에 공통되는 개념을 쉽게 추상화할 수 있다.

- **Persistence code** : 데이터를 데이터베이스 또는 코어 데이터에 저장하거나 디바이스에 데이터를 저장할 때 사용한다.

