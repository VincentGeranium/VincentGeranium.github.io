---
layout: post
title:  "CryptoKit(암호화폐 관련 개발 도구)"
date:   2019-06-07
categories: iOS, Swift
---

### 참고 자료

이 포스트는 이데일리 기사와 애플 도큐먼테이션을 참고로 하여 작성한 포스트임을 미리 밝힙니다

[이데일리 기사](https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=105&oid=018&aid=0004396394)

[Apple Documentation](https://developer.apple.com/documentation/cryptokit)

---

# CryptoKit

아이폰 등에 암호화폐 저장 기능 탑재할 수 있는 지원 기능

블록체인 연결과 전자지갑 기능을 더하는 개발자 도구

**암호화폐 관련 개발 도구**

공개 키 생성, 키 교환 등 암호화폐 전송과 저장을 위한 기능을 지원, 대칭키 암호(symmetric key)등 보안 기능도 갖추었다.

---

# Apple Documentataion of CryptoKit

애플 도큐먼테이션에 나와있는 CryptoKit을 번역한 내용입니다

- Framework

- Summary : 암호화 작업을 안전하고 효율적으로 수행

- 2019.06.07 기준 현재 베타 버전

- SDKs -> iOS 13.0+ (Beta), macOS 10.15+ (Beta), UIKit for Mac 13.0+ (Beta), tvOS 13.0+ (Beta)

## Overview

Apple CryptoKit을 사용하여 일반적인 암호화 작업 수행

- 암호화된 보안 다이제스트를 계산하고 비교

- 공개 키 암호화를 사용하여 디지털 서명을 작성 및 평가하고 키 교환을 수행, 메모리에 저장된 키로 작업하는 것 외에도 Secure Enclave에 저장되고 관리되는 개인 키를 사용가능

- 대칭 키를 생성하고 메시지 인증 및 암호화 같은 작업에 사용

CryptoKit은 앱이 원시 포인터 관리하는 것을 자유롭게 하고, 메모리 할당 해제 중에 중요한 데이터를 덮어쓰는 것과 같이 앱을 더 안전하게 만드는 작업을 자동으로 처리함.

---

# Cryptographically Secure Hashes

![image1](https://user-images.githubusercontent.com/42841888/59081555-b7185380-8929-11e9-9c27-f75b8ada23be.png)

---

# Message Authentication Codes

![image2](https://user-images.githubusercontent.com/42841888/59081569-c7c8c980-8929-11e9-81db-e007d5f724f8.png)

---

# Ciphers

![image3](https://user-images.githubusercontent.com/42841888/59081581-d3b48b80-8929-11e9-86bf-23257387b5ab.png)

---

# Public-Key Cryptography

![image4](https://user-images.githubusercontent.com/42841888/59081588-e038e400-8929-11e9-83ab-a74a437f37f9.png)

---

# Errors

![image5](https://user-images.githubusercontent.com/42841888/59081600-ed55d300-8929-11e9-92b2-1981b106f57f.png)

---

# Legacy Algorithms

![image6](https://user-images.githubusercontent.com/42841888/59081612-f9da2b80-8929-11e9-9a94-3f6b972a29f3.png)
