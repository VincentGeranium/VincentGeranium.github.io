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

<img width="200" alt="takePhoto" scr="https://user-images.githubusercontent.com/42841888/64150730-cd1fac80-ce63-11e9-92db-9e3e51905e13.PNG">

- 사진을 찍은 후 메인 View에 나타난 찍은 사진

<img width="200" alt="takePhoto_2" scr="https://user-images.githubusercontent.com/42841888/64150770-e58fc700-ce63-11e9-8b83-1f35b5175ff6.PNG">

- save 버튼을 눌러 디바이스 내의 커스텀 앨범을 따로 만들어 저장

<img width="200" alt="savePhoto" scr="https://user-images.githubusercontent.com/42841888/64150812-fd674b00-ce63-11e9-8c88-1ae4a12ac39e.PNG">

- 커스텀 앨범에 저장된 사진

<img width="200" alt="saveInCustomAlbum" scr="https://user-images.githubusercontent.com/42841888/64150860-17089280-ce64-11e9-9afb-c28e20573c35.PNG">

- Upload 버튼을 눌러 Firebase DB에 사진 올리기

<img width="200" alt="saveToDB" scr="https://user-images.githubusercontent.com/42841888/64150896-2982cc00-ce64-11e9-9c2d-b87109f0d2ce.PNG">

- firebase의 DB에 저장된 모습

<img width="1623" height="705" alt="firebaseDB" scr="https://user-images.githubusercontent.com/42841888/64150929-3c959c00-ce64-11e9-955f-5d66eba933e5.png">

- firebase의 storage에 저장된 모습

<img width="1548" height="676" alt="firebaseStorage" scr="https://user-images.githubusercontent.com/42841888/64151040-7ff00a80-ce64-11e9-85d3-34fc5910b1ad.png">

- Download 버튼을 눌러 firebase DB에서 이미지를 가저온 모습

<img width="200" alt="downloadFromDB" scr="https://user-images.githubusercontent.com/42841888/64151101-a150f680-ce64-11e9-8519-cd190f014e50.PNG">

---

### 완성된 앱 코드 in github

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/uplodaUsedFirebaseStorage)