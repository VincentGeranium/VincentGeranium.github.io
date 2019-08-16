---
layout: post
title:  "앱 생명주기"
date:   2019-08-16
categories: Swift, iOS
---

# App Life cycle

## iOS 앱 에서의 상태 변화

### 1. Not Running
    
    실행되지 않았거나, 시스템에 의해 종료된 상태
    
### 2. Inactive
    
    실행 중이지만 이벤트를 받고있지 않은 상태.
    
#### inactive 예시를 통한 설명

    앱 실행 중 미리알림 또는 일정 얼럿이 화면에 덮여서 앱이 실질적으로 이벤트를 받지 못하는 싱태
    
### 3. Active
    
    어플리케이션이 실질적으로 활동하고 있는 상태.

### Inactive와 Active 상태

    Inactive와 Active 상태는 앱의 상태 변화에 따라 혹은 상황에 따라 계속해서 상태의 변화가 이루어진다
    
    또한 Inactive와 Active 상태를 묶어 "Foreground" 라고 한다
    

앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있고, 상태 변화에 따라 다른 동작을 처리하기 위한 델리게이트 메서드들을 설명하시오.