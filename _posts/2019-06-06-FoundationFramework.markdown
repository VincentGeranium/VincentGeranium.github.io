---
layout: post
title:  "Foundation Framework에 대한 간략한 정리"
date:   2019-06-06
categories: Swift, iOS
---

### 참고 자료

이 포스트는 edwith의 iOS 부스트코스 강좌를 듣고 나서 정리된 내용을 참고하여 정리한 포스트임을 미리 밝힙니다.

[edwith iOS 부스트코스](https://www.edwith.org/boostcourse-ios/lecture/17996/)

---

# Foundation Framework

- Cocoa Touch Framework에 포함된 Framework = Foundation Framework

- Foundation Framework는 iOS application의 운영체제 서비스와 기본 기능을 포함하는 Framework

---

# What is the Foundation Framework

- Foundation은 원시 데이터 타입(String, Int, Double), 컬렉션 타입(Array, Dictionary, Set) 및 운영체제 서비스를 사용해 application의 기본적인 기능을 관리하는 Framework.

- Foundation Framework는 데이터 타입, 날짜 및 시간 계산, 필터 및 정렬, 네트워킹 등의 기본 기능을 제공

- Foundation Framework에서 정의한 클래스, 프로토콜 및 데이터 타입은 iOS 뿐만 아니라 macOS, watchOS, tvOS 등 모든 애플 SDK에서 사용된다

**Foundation Framework에서 제공하는 데이터 타입 및 컬렉션 타입의 대부분은 Objective-C 언어의 기능에서 지원하지 않는 것이기 때문에 언어기능을 보완하기 위한 구현이며, Swift에서는 이에 해당하는 데이터 타입과 기능 대부분을 Swift 표준 라이브러리에서 제공**

---

# Foundation Framework 기능별 요소

## 기본

- Number, Data, String : 원시 데이터 타입 사용

- Collection : Array, Dictionary, Set 등과 같은 컬렉션 타입 사용

- Date and Time : 날짜와 시간을 계산하거나 비교하는 작업

- Unit and Measurement :  물리적 차원을 숫자로 표현 및 관련 단위 간 변환 기능

- Data Formatting : 숫자, 날짜, 측정값 등을 문자열로 변환 또는 반대 작업

- Filter and Sorting : 컬렉션의 요소를 검사하거나 정렬하는 작업

## 애플리케이션 지원

- Resources : 애플리케이션의 에셋과 번들 데이터에 접근 지원

- Notification : 정보를 퍼트리거나 받아들이는 기능 지원

- App Extension : 확장 애플리케션과의 상호작용 지원

- Error and Exceptions : API와의 상호작용에서 발생할 수 있는 문제 상황에 대처할 수 있는 기능 지원

## 파일 및 데이터 관리

- File System : 파일 또는 폴더를 생성하고 읽고 쓰는 기능 관리

- Archives and Serialization :  속성 목록, JSON, 바이너리 파일들을 객체로 변환 또는 반대 작업 관리

- iCloud : 사용자의 iCloud 계정을 이용해 데이터를 동기화하는 작업 관리

## 네트워킹

- URL Loading System : 표준 인터넷 프로토콜을 통해 URL과 상호작용하고 서버와 통신하는 작업

- Bonjour : 로컬 네트워크를 위한 작업
