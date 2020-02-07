---
layout: post
title:  "Performing Operations with Objects in a Fetch Result"
date:   2020-02-07
categories: iOS, Swift
---

여러개의 FetchResult<PHAssetCollection>의 결과값이 여러개일 경우, 
    
이 PHFetchResult<PHAssetCollection>의(복수의 PHFetchResult<PHAssetCollection>) objects의 범위를 결정하여
    
그 범위에 맞는 PHAssetCollection들을 가져 올 수 있다

![FetchResultSummaryImage-1]()

그 외에도 가져 올 수 있는 방법이 여러가지가 있다 그 방법은 직접 Documentation을 찾아보길 바란다.

다시 본론으로 돌아와 위와 같은 방법으로 PHAssetCollection(복수)들을 가져와 내가 원하는 fetchOption의(sort 혹은 predicate) 

PHFetchResutl<PHAsset>을 뽑아내어 그 PHFetchResult<PHAsset>의 object 범위를 결정해 하나의 PHAsset을 가져와 image manger의 request image를 통하여 UIImage로 바꾸어 대표 thumbnail로 만들 수 있다
    
지금 현재 그러한 과정을 거치는 중에 풀지 못하는 부분이 있는데

여러 Collection을 가져오고 loop를 통하여 그것들의 PHAsset을 가져오고 그 image들을 각 셀에 넣어주려는 과정중 계속해서 오류가 난다

loop를 돌리는 과정에서 오류가 나는데 그것을 해결하기 위한 방법을 공부하던 중 Performing Operations with Objects in a Fetch Result을 사용하여 해결하면 되겠다는 생각을 했다




