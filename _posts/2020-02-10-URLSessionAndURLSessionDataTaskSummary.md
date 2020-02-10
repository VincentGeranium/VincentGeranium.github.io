---
layout: post
title:  "URLSession And URLSessionDataTask Summary"
date:   2020-02-10
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - URLSession과 URLSessionDataTask](https://www.edwith.org/boostcourse-ios/lecture/16863/)

- - -

### URLSession And URLSessionTask

- - -

### 간단 정리

#### URLSession

- HTTP/HTTPS를 통해 콘텐츠(데이터)를 주고받기 위해 API를 제공하는 클래스

#### URLSessionTask

- 세션 작업을 하나로 나타내는 클래스

- - -

### About URLSession

- HTTP/HTTPS를 통해 콘텐츠(데이터)를 주고받기 위해 API를 제공하는 클래스

- 이 API는 인증 지원을 위한 많은 델리게이트 메서드를 제공
    
- 애플리케이션이 실행 중이지 않거나 일시 중단된 동안 백그라운드 작업을 통해 콘텐츠를 다운로드 하는 것을 수행하기도 한다

- URLSession API를 사용하기 위해 애플리케이션은 세션을 생성한다

- 해당 세션은 관련된 데이터 전송작업 그룹을 조정한다

    - 예를 들면 웹 브라우저를 사용 중인 경우 탭 당 하나의 세션을 만들 수 있다

    - 각 세션 내에서 애플리케이션은 작업을 추가하고, 각 작업은 특정 URL에 대한 요청을 나타낸다

![URLSessionImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/URLSessionImage-1.png?raw=true)


#### Request

- 서버로 요청을 보낼 때 어떤 (HTTP)메서드를 사용할 것인지, 캐싱 정책은 어떻게 할 것인지 들의 설정을 할 수 있다

#### Response

- URL 요청의 응답을 나타내는 객체

#### 세션의 유형

- URLSession API는 세가지 유형의 세션을 제공한다.

- 이 타입은 URLSession 객체가 소유한 configuration 프로퍼티 객체에 의해 결정된다

#### 1) 기본 세션 (Default Session)

- 기본 세션은 URL 다운로드를 위한 다른 파운데이션 메서드와 유사하게 동작한다. 디스크에 저장하는 방식이다.
    
#### 2) 임시 세션 (Ephemeral Session)

- 기본 세션과 유사하지만, 디스크에 어떤 데이터도 저장하지 않고, 메모리에 올려 세션과 연결한다. 따라서 애플리케이션이 세션을 만료시키면 세션과 관련한 데리터가 사라진다.
    
#### 3) 백그라운드 세션 (Background Session)

- 백그라운드 세션은 별로도 프로세스가 모든 데이터 전송을 처리한다는 점을 제외하고는 기본 세션과 유사하다.
    
#### 세션 만들기

- init(configuration:) : 지정된 세션 구성으로 세션을 만든다

```swift
init(configuration: URLSessionConfiguration)
```

- shared : 싱글턴 세션 객체를 반환한다

```swift
class var shared: URLSession { get }
```

#### 세션 구성

- configuration : 이 세션에 대한 구성 객체이다

```swift
@NSCopying var configuration: URLSessionConfiguration { get }
```

- delegate : 이 세션의 델리게이트이다

```swift
var delegate: URLSessionDelegate? { get }
```

- - -

### Task

- URLSessionTask는 세션 작업 하나를 나타내는 추상 클래스이다

- 하나의 세션 내에서 URLSession 클래스는 세 가지 작업 유형, 즉 데이터 작업(Data Task), 업로드 작업(Upload Task), 다운로드 작업(Download Task)을 지원한다

#### 1) URLSessionDataTask

- HTTP의 각종 메서드를 이용해 서버로부터 응답 데이터를 받아서 Data 객체를 가져오는 작업을 수행한다

#### 2) URLSessionUploadTask

- 애플리케이션에서 웹 서버로 Data 객체 또는 파일 데이터를 업로드하는 작업을 수행한다

- 주로 HTTP의 POST 혹은 PUT 메서드를 이용한다

#### 3) URLSessionDownloadTask

- 서버로부터 데이터를 다운로드 받아서 파일의 형태로 저장하는 작업을 수행한다

- 애플리케이션의 상태가 대기 중이거나 실행 중이 아니라면 백그라운드 상태에서도 다운로드가 가능하다

#### 데이터 작업과 업로드 작업 및 다운로드 작업

- 데이터 작업은 서버로부터 어떤 응답이라도 Data 객체의 형태로 전달받을 떄 사용

- 업로드 작업 및 다운로드 작업은 단순한 바이너리 파일의 전달에 목적을 둔다고 볼 수 있다

- JSON, XML, HTML 데이터 등 단순한 데이터의 전송에는 주로 데이터 작업을 사용한다

- 용량이 큰 파일의 경우 애플리케이션이 백그라운드 상태인 경우에도 전달 할 수 있도록 업로드(다운로드) 작업을 주소 사용한다

- - -

### 세션에 Data Task 추가하기

- dataTask(with:) : URL에 데이터를 요청하는 데이터 작업 객체를 만든다.

```swift
func dataTask(with url: URL) -> URLSessionDataTask
```

- dataTask(with:) : URLRequest 객체를 기반으로 URL에 데이터를 요청하는 데이터 작업 객체를 만든다.

```swift
func dataTask(with request: URLRequest) -> URLSessionDataTask
```

- dataTask(with:completionHandler:) : URL에 데이터를 요청하고 요청에 대한 응답을 처리할 완료 핸들러(Completion Handler)를 갖는 데이터 작업 객체를 만든다

```swift
func dataTask(with url: URL, completionHandler: @escaping(Data?, URLResponse?, Error?) -> Void) -> URLSessionDataTask
```

- dataTask(with:completionHandler:) : URLRequest 객체를 기반으로 URL에 데이터를 요청하고 요청에 대한 응답을 처리할 완료 핸들러(Completion Handler)를 갖는 데이터 작업 객체를 만든다

```swift
func dataTask(with request: URLRequest, completionHandler: @escaping(Data?, URLResponse?, Error?) -> Void) -> URLSessionDataTask
```

- - -

### 세션에 Download Task 추가하기

- downloadTask(with:) : URL에 요청한 데이터를 다운로드 받아서 파일에 저장하는 다운로드 작업을 만든다

```swift
func downloadTask(with url: URL) -> URLSessionDownloadTask
```

- downloadTask(with:completionHandler:) : URL에 요청한 데이터를 다운로드 받아서 파일에 저장하고 저장 완료 후 완료 핸들러를 호출하는 다운로드 작업을 만든다

```swift
func downloadTask(with url: URL, completionHandler: @escaping(URL?, URLResponse?, Error?) -> Void) -> URLSessionDownloadTask
```

- downloadTask(with:) : URLRequest 객체를 기반으로 URL에 요청한 데이터를 다운로드 받아서 파일로 저장하는 다운로드 작업을 만든다

```swift
func downloadTask(with request: URLRequest) -> URLSessionDownLoadTask
```

- downloadTask(with:completionHandler:) : URLRequest 객체를 기반으로 URL에 요청한 데이터를 다운로드 받아서 파일로 저장하고 완료 후 핸들러를 호출하는 다운로드 작업을 만든다

```swift
func downloadTask(with request: URLRequest, completionHandler: @escaping(URL?, URLResponse?,Error?) -> Void) -> URLSessionDownloadTask
```

- - -

### 세션에 Upload Task 추가하기

- uploadTask(with:from:) : URLRequest 객체를 기반으로 URL에 데이터를 업로드하는 작업을 만든다

```swift
func uploadTask(with request: URLRequest, from bodyData: Data) -> URLSessionUploadTask
```

- uploadTask(with:from:completionHandler:) : URLRequest 객체를 기반으로 URL에 데이터를 업로드하고 업로드 완료 후 완료 핸들러를 호출하는 작업을 만든다

```swift
func uploadTask(with request: URLRequest, from bodyData: Data?, completionHandler: @escaping(Data?, URLResponse?, Error?) -> Void) -> URLSessionUploadTask
```

- uploadTask(with:fromFile:) : URLRequest 객체를 기반으로 URL에 파일을 업로드하는 작업을 만든다

```swift
func uploadTask(with request: URLRequest, fromFile fileURL: URL) -> URLSessionUploadTask
```

- uploadTask(with:fromFile:completionHandler:) : URLRequest 객체를 기반으로 URL에 파일을 업로드하고 업로드 완료 후 완료 핸들러를 호출하는 업로드 작업을 만든다

```swift
func uploadTask(with request: URLRequest, fromFile fileURL: URL, completionHandler: @escaping(Data?, URLResponse?, Error?) -> Void) -> URLSessionUploadTask
```

- - -

### 작업(테스크) 상태 제어

- cancel() : 작업을 취소한다

```swift
func cancel()
```

- resume() : 일시중단된 경우 작업을 다시 시작한다

```swift
func resume()
```

- suspend() : 작업을 일시적으로 중단한다

```swift
func suspend()
```

- state : 작업의 상태를 나타낸다

```swift
var state: URLSessionTask.State { get }
```

- priority : 작업처리 우선순위이다. 0.0부터 1.0 사이이다.

```swift
var priority: Float { get set }
```