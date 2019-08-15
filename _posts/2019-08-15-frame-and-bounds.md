---
layout: post
title:  "Frame과 Bounds의 차이 정리"
date:   2019-08-15
categories: Swift, iOS
---

# Frame

    UIView의 instance property
    
    origin과 size를 갖는다 -> x, y, width, height를 갖는다

#### "SuperView의 좌표 시스템" 안에서 View의 위치와 크기를 나타낸다

    SuperView(상위뷰) = 한단계 위의 상위뷰를 의미함
    
# Bounds
    
    UIView의 instance property
    
    origin과 size를 갖는다 -> x, y, width, height를 갖는다
    
#### View의 위치와 크기를 "자신만의 죄표 시스템" 안에서 나타낸다

    bounds의 핵심 = 자신만의 좌표 시스템을 사용