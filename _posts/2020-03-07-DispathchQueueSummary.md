---
layout: post
title:  "Pagination TableView Summary"
date:   2020-03-07
categories: iOS, Swift
---

Pagination이 가능한 TableView를 만들면서 배운점에 관하여 Summary 했습니다.

아래의 영상을 보며 예제 코드를 만들며 공부했습니다.

[Pagination with UITableVIew - Load more content UITableView - Swift 4](https://www.youtube.com/watch?v=WVjU75BoUKE)

예제 코드

[Vincent Example Code About Pagination with UITableView - Load more content UITableView](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-06-pagination-tableView)

- - -

### Summary

![PaginationWithUITableViewImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PaginationWithUITableViewImage-1.png?raw=true)

- 위의 그림에서 보면 `recordsArray` 가 비어있는데 이 곳에 데이터가 쌓인다고 생각하면 된다.
    
![PaginationWithUITableViewImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PaginationWithUITableViewImage-2.png?raw=true)

- UITableView의 method 중 `tableView(_:willDisplay:forRowAt:)`을 사용한다

- `tableView(_:willDisplay:forRowAt:)`는 델리게이트에게 테이블 뷰가 특정 행에 대한 셀을 그리려고 한다는 것을 알려준다.

- 위의 그림에서 `if문`을 보면 `indexPath.row == recordsArray.count - 1`로 되어있다.

    - 즉, indexPath.row와 recordsArray.count 행과 데이터의 갯수가 맞으면 더 많은 컨텐츠를 불러올수 있으므로 if 문 아래의 코드가 실행되게 한다.
    
- 다음 `if문`을 보면 `recordsArray.count < serverTotalEntries`로 되어있다.

    - `즉, 데이터가 들어와 저장된 공간의 갯수(데이터의 갯수)가 서버가 제공하는 총 데이터의 갯수보다 작다면 아직 데이터를 더 가져와 로드 해 줄수 있다는 뜻이다.`
    
- `if문`안에 코드를 보면 처음 apiLimit(20)에 맞게 들어가 있는 recordsArray의 데이터 갯수(20개)를 인덱스로 사용하였다.

- 그리고 apiLimit을 20개씩 늘려준다

- 다음 `while문`을 보면 `index < apiLimit`으로 되어 있다. 
    
- `apiLimit은` 계속해서 `recordsArray.count + 20`으로 커져간다.
    
- 그리고 `index`는 1씩 늘어가며 `recordsArray`에 쌓여간다.
    
- 그러나 가장 중요한것은 맨 처음 `if문`인데 `serverTotalEntries`보다 `recoedsArray.count` 크면 더 이상의 데이터를 가져올게 없으므로 셀을 더이상 그려주지 않는다

    - 즉, 구문이 종료된다는 말이다.