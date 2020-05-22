---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 1 (Bounds 와 Frame 의 차이점)"
date:   2020-05-22
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [zeddios - Frame과 Bounds의 차이 (1/2)](https://zeddios.tistory.com/203)

- [zeddios - Frame과 Bounds의 차이 (2/2)](https://zeddios.tistory.com/231)

- - -
- - -

### Bounds 와 Frame 의 차이점

- Frame과 Bounds는 UIView의 instance property.

    - Frame과 Bounds는 사각형으로 그려짐.
    
        - 즉, origin과 size를 가진다.
        
        - 즉, x좌표, y좌표, width, height를 가진다.

- Frame

    - SuperView(상위뷰)의 좌표시스템 안에서 View의 위치와 크기를 나타낸다.
    
    - frame의 가장 중요한 포인트 -> SuperView의 좌표시스템.
    
    - 자신의 부모뷰(SuperView, 상위뷰)를 기준으로 origin의 위치를 정하는것이 frame.
    
    - 위치와 크기를 정해줄 때 사용. Frame은 위치가 포인트.
    
- Bounds

    - View의 위치와 크기를 자신만의 좌표시스템 안에서 나타낸다.
    
    - bounds의 가장 중요한 포인트 -> 자신만의 좌표시스템.
    
    - 상위뷰(SuperView)와 아무런 상관이 없으며, 오직 자신이 기준인것.
    
    - 자신만의 좌표계를 기준으로 위치(x,y) 및 크기(width, height)로 표현되는 사각형
    
        - 그래서 bounds의 origin은 default로 (0,0)이다.
        
    - Bounds는 상위뷰 안에서의 좌표가 아닌 자신만의 좌표시스템을 가진다. Bounds를 변경하는 것은 해당 위치에서 View를 다시 그리라는 의미가 된다. Bounds는 상위뷰와 아무런 관련이 없다.
    
    - Bounds는 View의 크기만 변경할 수 있다. Bounds에는 위치정보가 없다.
    
- Frame와 Bounds의 사용

    - Frame
        
        - UIView 위치나 크기를 설정하는 경우.
    
    - Bounds
        
        - View 내부에 그림을 그릴 때 (drawRect).
        
        - transfomation 후, View의 크기를 알고싶을 때.
        
        - 하위 View를 정렬하는 것과 같이 내부적으로 변경하는 경우.