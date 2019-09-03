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

<img width="200" alt="takePhoto" scr="https://vincentgeranium.github.io/assets/img/takePhoto.PNG">


- 사진을 찍은 후 메인 View에 나타난 찍은 사진

<img width="200" alt="takePhoto_2" scr="https://vincentgeranium.github.io/assets/img/takePhoto_2.PNG">

- save 버튼을 눌러 디바이스 내의 커스텀 앨범을 따로 만들어 저장

<img width="200" alt="savePhoto" scr="https://vincentgeranium.github.io/assets/img/savePhoto.PNG">

- 커스텀 앨범에 저장된 사진

<img width="200" alt="saveInCustomAlbum" scr="https://vincentgeranium.github.io/assets/img/saveInCustomAlbum.PNG">

- Upload 버튼을 눌러 Firebase DB에 사진 올리기

<img width="200" alt="saveToDB" scr="https://vincentgeranium.github.io/assets/img/saveToDB.PNG">

- firebase의 DB에 저장된 모습

<img width="3246" height="1410" alt="firebaseDB" scr="https://vincentgeranium.github.io/assets/img/firebaseDB.png">

- firebase의 storage에 저장된 모습

<img width="3246" height="1410" alt="firebaseStorage" scr="https://vincentgeranium.github.io/assets/img/firebaseStorage.png">

- Download 버튼을 눌러 firebase DB에서 이미지를 가저온 모습

<img width="200" alt="downloadFromDB" scr="https://vincentgeranium.github.io/assets/img/downloadFromDB.PNG">

---

### 완성된 앱 코드 in github

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/uplodaUsedFirebaseStorage)