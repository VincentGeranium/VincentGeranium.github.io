---
layout: post
title:  "firebase 앱 완성"
date:   2019-09-03
categories: iOS, Swift
---

#### 아래의 포스트들과 이어지는 내용 입니다

1. [Image Picker 사용, 디바이스 카메라로 사진 찍고, 앨범에 저장](https://vincentgeranium.github.io/ios,/swift/2019/08/28/til.html)

2. [사진 저장을 커스텀 앨범에 하기](https://vincentgeranium.github.io/ios,/swift/2019/08/30/til.html)

3. [FireBase에 사진 업로드 하기](https://vincentgeranium.github.io/ios,/swift/2019/08/31/uploadImageToFireBase.html)

---

- 디바이스의 카메라를 이용하여 사진 찍기

![takePhoto](https://user-images.githubusercontent.com/42841888/64230684-792acb80-cf28-11e9-8ecc-5971312cfe1a.PNG)

- 사진을 찍은 후 메인 View에 나타난 찍은 사진

![takePhoto_2](https://user-images.githubusercontent.com/42841888/64230654-60221a80-cf28-11e9-875a-1e0c7d6b306b.PNG)

- save 버튼을 눌러 디바이스 내의 커스텀 앨범을 따로 만들어 저장

![savePhoto](https://user-images.githubusercontent.com/42841888/64230614-4385e280-cf28-11e9-8674-f96137f02dd3.PNG)

- 커스텀 앨범에 저장된 사진

![saveInCustomAlbum](https://user-images.githubusercontent.com/42841888/64230581-30731280-cf28-11e9-8f28-f43261715b09.PNG)

- Upload 버튼을 눌러 Firebase DB에 사진 올리기

![saveToDB](https://user-images.githubusercontent.com/42841888/64230562-1fc29c80-cf28-11e9-85aa-070183f44caf.PNG)

- firebase의 DB에 저장된 모습

<img width="1623" alt="firebaseDB" src="https://user-images.githubusercontent.com/42841888/64229776-c22d5080-cf25-11e9-9e29-cb349178871f.png">

- firebase의 storage에 저장된 모습

<img width="1548" alt="firebaseStorage" src="https://user-images.githubusercontent.com/42841888/64229638-47643580-cf25-11e9-8d97-2af69dca8fa6.png">

- Download 버튼을 눌러 firebase DB에서 이미지를 가저온 모습

![downloadFromDB](https://user-images.githubusercontent.com/42841888/64230523-03266480-cf28-11e9-889f-5d63641005fa.PNG)

---

### 완성된 앱 코드 in github

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/uplodaUsedFirebaseStorage)