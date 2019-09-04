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

<img width="200" alt="takePhoto" scr="https://user-images.githubusercontent.com/42841888/64230191-0ff68880-cf27-11e9-993d-794961703808.PNG">

- 사진을 찍은 후 메인 View에 나타난 찍은 사진

<img width="200" alt="takePhoto_2" scr="https://user-images.githubusercontent.com/42841888/64229813-dbce9800-cf25-11e9-92aa-b6d0ee802d4b.PNG">

- save 버튼을 눌러 디바이스 내의 커스텀 앨범을 따로 만들어 저장

<img width="200" alt="savePhoto" scr="https://user-images.githubusercontent.com/42841888/64230131-e4739e00-cf26-11e9-872f-2be2016ca987.PNG">

- 커스텀 앨범에 저장된 사진

<img width="200" alt="saveInCustomAlbum" scr="https://user-images.githubusercontent.com/42841888/64230115-cefe7400-cf26-11e9-91f6-1e20c216dc41.PNG">

- Upload 버튼을 눌러 Firebase DB에 사진 올리기

<img width="200" alt="saveToDB" scr="https://user-images.githubusercontent.com/42841888/64230025-88a91500-cf26-11e9-842e-3fdf37cb625d.PNG">

- firebase의 DB에 저장된 모습

<img width="1623" alt="firebaseDB" src="https://user-images.githubusercontent.com/42841888/64229776-c22d5080-cf25-11e9-9e29-cb349178871f.png">

- firebase의 storage에 저장된 모습

<img width="1548" alt="firebaseStorage" src="https://user-images.githubusercontent.com/42841888/64229638-47643580-cf25-11e9-8d97-2af69dca8fa6.png">

- Download 버튼을 눌러 firebase DB에서 이미지를 가저온 모습

<img width="200" alt="downloadFromDB" scr="https://user-images.githubusercontent.com/42841888/64229991-62837500-cf26-11e9-9db6-a3a4a0cded01.PNG">

---

### 완성된 앱 코드 in github

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/uplodaUsedFirebaseStorage)