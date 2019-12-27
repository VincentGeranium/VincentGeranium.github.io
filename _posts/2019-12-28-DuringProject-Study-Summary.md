---
layout: post
title:  "프로젝트 진행 중 문제점 해결 (tableView.rowHeight)"
date:   2019-12-27
categories: iOS, Swift
---

### Custom TableViewCell의 높이 문제

WeatherToday 프로젝트를 진행하다가 생긴 문제점이

![customCellHeightErrorImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/customCellHeightErrorImage.png?raw=true)

위의 사진과 같이 constraint를 준 것들 중에 받아들여지지 않는(?) constraint를 찾아

고치기를 원한다는 메시지나 나왔다

나는 이 문제점이 어디서 생긴지 몰라 위의 메시지를 자세히 들여다보고

Custom Cell의 constraint를 하나씩 고쳐가보니 Cell의 heightAnchor Constraint를 150으로 준것이 잘못되어

위의 메시지가 나온것 이였다.

그리하여 Custom Cell의 heightAnchor Constraint를 지우니 메시지는 사라졌지만

테이블 뷰의 Cell이 뭉개져 나왔다.

- CustomCell이 뭉개져 나와 비정상적으로 작동하는 CustomTableView

![errorCellImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/errorCellImage.png?raw=true)

그리하여 이러한 뭉개짐을 고치기 위해 여러 삽질을 거듭하다 꼼꼼한 재은씨 기본편의 "커스텀 프로토타입 셀"의 챕터에서

테이블 뷰 전체에 일괄로 높이를 설정하는 방법(StoryBoard를 이용)를 설명해 주는 부분(P.540)을 보고

rowHeight 값을 주면 일괄로 높이가 조정이 되어 셀이 뭉개지지 않음을 알게 되었다 (나는 모든 코딩을 스토리보드 없이 코드로만 한다.)

그리하여 ViewController 안에 tableView 인스턴스를 생성후 그 tableView의 rowHeight 값을 주고 이 문제를 해결하였다

- 정상적으로 작동하는 CustomCell을 받아들인 CustomTableView

![normalCellImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/normalCellImage.png?raw=true)