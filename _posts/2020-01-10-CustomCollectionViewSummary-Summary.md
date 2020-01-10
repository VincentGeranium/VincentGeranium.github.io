---
layout: post
title:  "Custom CollectionView and Cell 만들며 배운점 Summary"
date:   2020-01-10
categories: iOS, Swift
---

### Cell 의 ImageView의 Image에 직접 접근하지 않기

![CV_CustomCell](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CV_CustomCell.png?raw=true)

예전에 WeatherToday Project(edwith project)를 진행할때는 따로 접근 제한을 두지 않아서 바로 cell의 imageView의 image에 접근하여 image를 넣어주었었다.

그러나 이번에 Custom CollectionView의 Cell의 image를 위의 사진과 같이 셀의 backImage를 fileprivate으로 접근을 제한 해두었다.

그리하여 이 내부에서만 접근이 가능하도록 하였다.

'그럼 어떻게 셀의 이미지에 접근하여 각기 다른 이미지를 보여줄 수 있을까?' 하고 생각하였었다.

이 프로젝트를 진행하면서 배운점이 바로 struct를 이용하여 data 타입을 따로 만들고 그것을 이용하여 메인 뷰컨과 커스텀 셀에서 사용하여 접근 할 수 있도록 하였다.

제일 먼저

![CustomDataImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CustomDataImage.png?raw=true)

위의 사진과 같이 커스텀 데이터 스트럭쳐를 만들고

![CustomCellImageData](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CustomCellImageData.png?raw=true)

커스텀 셀 클래스 내부에 CustomData? 타입의 imageData라는 프로퍼티를 만들어 놓고 didSet을 통하여 이 프로퍼티로 들어오는 CustomData 타입의 데이터 중 image를 customCell의 이미지로 주게 만들었다

이 커스텀 셀의 이미지는 didSet을 통하여 들어오는데 이 이미지는 메인 뷰컨을 통하여 이미지가 들어옴을 알 수 있다

![mainVCImageData](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mainVCImageData.png?raw=true)

메인 뷰컨에 와서 CustomData 타입의 배열을 만들어 이 안에 커스텀 셀의 이미지에 들어갈 여러 이미지들을 넣어준다

그 다음

![mainVCExtension](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mainVCExtension.png?raw=true)

```swift
cell.imageData = self.imageData[indexPath.item]
```

위와 같이 indexPath.item을 통하여 차례로 이미지가 CustomCell의 imageData로 들어가 didSet을 통하여 차례로 cell의 이미지로 들어가 지는 것이다

![DataFlowCustomCell](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/DataFlowCustomCell.jpg?raw=true)

- - -

### 부가적 설명

나는 tableView나 collectionView를 만들면서 항상 까먹는것이 있는데 바로 indexPath.row와 indexPath.item을 통하여 어떻게 데이터들을 접근 할 수 있는지 였다.

이 궁굼증은 zedd님의 블로그를 자주 보며 공부하였다 아래에 링크를 올려두겠다.

[zedd님 - tableViewController 관련 포스트](https://zeddios.tistory.com/54)

또한 위 프로젝트의 소스코드도 올려두겠다.

[VincentGeranimu - CustomCollectionView Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-01-09-CvCellExample)

링크는 올려져있지만 이 포스트는 나의 공부를 위한 포스트임으로 다시 한번 정리해 보겠다

위의 그림에서 보면

메인 뷰컨에 ```swift imageData: [CustomData] = [CustomData(title: "bikeTire", image: #imageLiteral(resourceName: "bikeTire"), url: "freeImage.com/bikeTire"),...]```

식으로 4가지의 이미지가 들어있는데

```swift imageData[indexPath.item]``` 으로 접근한다고 해서 imageData의 원소들에 어떻게 접근하는지 알 수 없엇다

```swift
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        guard let cell: CustomCollectionViewCell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath) as? CustomCollectionViewCell else {
            return UICollectionViewCell()
        }
       
        cell.imageData = self.imageData[indexPath.item]
        return cell
    }
```  

내부에 print로 function call이라는 문자를 몇번 나타내는지 넣어보면 imageData의 배열의 원소 갯수만큼 function call이 불리어지는 것을 확인할수있었다

그 후에는 그럼 indexPath를 프린트 해 보았는데 [0, 0], [0, 1], [0, 2], [0, 3] 가 나왔다

indexPath.item을 프린트 해 보았는데 0, 1, 2, 3 이 나왔다

이것으로 알 수 있는것은

indexPath.item은 indexPath의 두 번째에 위치한 값 즉 [0, 0], [0, 1], [0, 2], [0, 3] 중 0, 1, 2, 3을 가져온것이다

그렇다면 우리가 imageData[indexPath.item]으로 접근을하게 되면

imageData 배열의 첫 번째 원소부터 접근이 된다고 알 수 있다

여기서 또 중요한 점이 있는데 indexPaht가 [?,item]으로 이루어져 있다는 것을 알 수 있었는데

이 ?의 값은 section을 의미한다

이 프로젝트에서는 section을 따로 주지 않았다 그래서 0번째 섹션밖에 없는것이다

그러면 **indexPath는 [section,item]로 이루어져 있는 행을 식별하는 상대적인 경로**라고 볼 수 있는것이다.