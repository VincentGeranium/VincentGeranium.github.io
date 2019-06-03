---
layout: post
title:  "AVFoundation, Timer -> edwith 강의 듣고 강의 자료 참고하여 정리"
date:   2019-06-03
categories: Swift, iOS
---

# 출처

이 포스트는 edwith의 부스트코스 iOS 프로그래밍 과정 중 **음원 재생기 애플리게이션 - 6) 구현 코드 작성하기**를 학습하고 난 뒤 위의 과정을 참고하여 작성한 포스트 임을 미리 밝힙니다.

---

# AVFoundation

**AVFoundation은** 다양한 Apple 플랫폼에서 **사운드 및 영상 미디어의 처리, 제어, 가져오기 및 내보내기 **등 광범위한 기능을 하는 **프레임워크**

# AVFoundation의 주요 기능

- 미디어 재생 및 편집

- 디바이스의 카메라와 마이크를 이용한 영상 녹화 및 사운드 녹음

- 시스템 사운드 제어

- 문자의 음성화

---

# AVAudioPlayer Class란

AVAudioPlayer 클래스는 파일 또는 메모리에 있는 사운드 데이터를 재생하는 기능을 제공

# AVAudioPlayer의 주요 기능

- 파일 또는 메모리에 있는 사운드 재생(네트워크에 있는 사운드 파일은 재생 불가)

- 파일 재생 시간 길이의 제한 없이 사운드 재생

- 여러 개 사운드 파일 동시 재생

- 사운드 재생 속도 제어 및 스테레오 포지셔닝

- 앞으로 감기와 뒤로 감기 등의 기능을 지원해 사운드 파일의 특정 지점 찾기

- 현재 재생 정보 데이터 얻기

- 사운드 반복 재생 기능

# AVAudioPlayer 주요 프로퍼티

- var isPlaying: Bool -> 사운드가 현재 재생되고 있는지 아닌지 여부

- var volum: Float -> 사운드의 볼륨 값, 최소 0.0 ~ 최대 1.0

- var rate: Float -> 사운드의 재생 속도

- var numberOfLoops: Int -> 사운드 재생 반복 횟수
    - 기본값 -> 0, 사운드 1회 재생 후 종료
    - 양수값으로 설정시 설정값 +1 회 재생 -> 예를들어 1로 설정시 2회 재생 후 종료
    - 음수값으로 설정시 stop 메서드가 호출 될때까지 무한 재생

- var dutation: TimeInterval -> 사운드의 총 재생 시간 (초단위)

- var currentTime: TimeInterval -> 사운드의 현재 재생 시각 (초단위)

- protocol AVAudioPlayerDelegate -> 사운드 재생 완료, 재생 중단 및 디코딩 오류에 응답할 수 있는 프로토콜

# AVAudioPlayer 주요 메서드

- AVAudioPlayer 초기화 메서드

```
// 특정 위치에 있는 사운드 파일로 초기화
func init(contentOf: URL)


// 메모리에 올라와있는 데이터를 이용해 초기화
func init(data: data)
```

- AVAudioPlayer 재생관련 메서드

```
// 사운드 재생
func play()


// 특정 시점에서 사운드 재생
func play(atTime: TimeInterval)


//사운드 일시 정지
func pause()


//사운드 재생 정지
func stop()
```

---

# Timer

**Timer 클래스는 일정한 시간 간격이 지나면 지정된 메시지를 특정 객체로 전달하는 기능 제공**

---

# Timer 주요 프로퍼티

- var isVaild: Bool -> 타이머가 현재 유효한지 아닌지 여부

- var fireDate: Date -> 다음에 타이머가 실행될 시각

- var timeInterval: TimeInterval -> 타이머의 실행 시간 간격 (초단위)

---

# Timer 생성 메서드

- 타이머 생성과 동시에 런 루프에 default mode로 등록하는 클래스 메서드

```
class func scheduledTimer(withTimeInterval: TimeInterval, repeats: Bool, block: (time) -> Void)

class func scheduledTimer(timeInterval: TimeInterval, target: Any, selectop: Selector, userInfo: Any?, repeats: Bool)

class func scheduledTimer(timeInterval: TimeInterval, invocation: NSInvocation, repeats: Bool)
```

- 타이머 생성 후 수동으로 타이머 객체를 add(_:forMode:) 메서드를 이용해 런 루프에 추가해줘야 하는 메서드

```
func init(timeInterval: TimeInterval, invocation: NSInvocation, repeats: Bool)

func init(timeInterval: TimeInterval, target: Any, selector: Selector, userInfo: Any?, repeats: Bool)

func init(fireAt: Date, interval: TimeInterval, target: Any, selector: Selector, userInfo: Any?, repeats: Bool)
```

---

#### 실습 자료

[VincentGeranium Github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-05-29-MusicPlayer)
