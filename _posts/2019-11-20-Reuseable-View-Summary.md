---
layout: post
title:  "뷰의 재사용 Summary"
date:   2019-11-20
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - 뷰의 재사용이란?](https://www.edwith.org/boostcourse-ios/lecture/16891/)

- - -

### 뷰의 재사용

- iOS 기기는 한정된 메모리를 가지고 애플리케이션을 구동함

- 만약 사용자에게 보여주고 싶은 데이터가 매우 많고, 데이터의 양만큼 많은 뷰가 필요하다면??

    - 화면에 표시할 수 있는 뷰의 개수는 한정되어 있지만, 표현해야 하는 데이터가 많은 경우 반복된 뷰를 생성하기보다는 뷰를 재사용
    
    - 사용할 수 있는 메모리가 작아서 데이터의 양만큼 많은 뷰를 생성하는 것은 메모리를 많이 낭비하는것
    
    - 그러므로 뷰를 재사용하여 메모리 절약, 성능 향상의 두가지 이점을 얻을 수 있다
    
- - -

### 재사용의 대표적인 예

- iOS 환경에서 뷰를 재사용하는 대표적인 예

    - 1) UITableViewCell -> UITableView의 셀
    
    - 2) UICollectionViewCell -> UICollectionView의 셀
    
- - -

### 재사용 원리

- 1) 테이블뷰 및 컬렉션뷰에서 셀을 표시하기 위해 데이터 소스에 뷰(셀) 인스턴스를 요청

- 2) 데이터 소스는 요청마다 새로운 셀을 만드는 대신 `재사용 큐(Reuse Queue)`에 재사용을 위해 대기하고있는 셀이 있는지 확인 후 있으면 그 셀에 새로운 데이터를 설정하고, 없으면 새로운 셀을 생성

- 3) 테이블뷰 및 컬렉션뷰는 데이터 소스가 셀을 반환하면 화면에 표시

- 4) 사용자가 스크롤을 하게 되면 일부 셀들이 화면 밖으로 사라지면서 다시 재사용 큐에 들어간다

- 5) 위의 1번부터 4번까지의 과정이 계속 반복된다

![reuseCellImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reuseCellImg.png?raw=true)
