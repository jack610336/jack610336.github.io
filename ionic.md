# Ionic 學習筆記

現在有越來越多的跨平台開發框架，Ionic即是其中一個，Ionic是一個可以跨平台做出hyperApp的框架
我們可以只寫一份code，然後分別發布到不同的手機中，Android、iOS，他可以幫我們build出 apk 和 ipa檔案，
這大大的縮短了我們開發App的時間，也可以讓更多web端的開發者能夠投入App開發，讓一些開發團隊也能夠減少人力資源，但是這不是一個萬靈丹，前面說了一堆優點，他也是有缺點存在的，再App的執行速度上比不上原生的Native App，再依些比較客製化的功能及UI上面也會比較難以實做出來。那我們廢話不多說開始來介紹一下怎麼安裝及建置Ionic的環境及開起第一個hello world專案。

下列環境建置於windows 10
首先需要安裝 node.js
所以先到官網(https://nodejs.org/en/) 下載並安裝後

打開cmd，打入下列指令後，應該可以看到目前的版本，表示我們已經安裝完成。
```
$ node --version
```
接下來我們要安裝 Cordova 和 Ionic 的 command-line tools

```
$ npm install -g cordova ionic
```

安裝好後我們也依樣可以利用--version 來確定是否有安裝成功並查看版本號

```
$ ionic --version

$ cordova --version
```

在這裡要強調一點，如果是想要發布iOS App就必須要有MacOS，所以在這篇介紹中，我們會介紹android 的部分。

首先我們來創建一個新專案，我們的練習題目是bmi，所以透過名稱我就叫他bmi，後面的tabs，是ionic 預設的UI樣式之一，有著三個分頁。
```
$ ionic start bmi_calculator tabs
```
當我們開好專案後，在進入我們的專案目錄，那可以依照自己的需求加入android 或是 iOS，
他會自動幫我們載入
```
$ cd ./bmi_calculator/
$ ionic cordova platform add ios     # if you're on macOS
$ ionic cordova platform add android # if you need to publish for android.
```
這時候我們可以直接 build 一個apk 試試看，只要像下面指令，打上build 就可以build出apk來
如果執行run的話，系統會幫我們build好並將檔案派送出去製手機或模擬器上直接執行。
```
$ ionic cordova build android        # build an android apk
$ ionic cordova run android          # build and run in a emulate or real phone
```

我們要如何debug呢? 在寫程式的時候，我們可以開啟測試伺服器，用下列指令就可以成功的開啟
下列的兩個指令都可以開啟，只是差別在預設開啟網頁的不同而已，大家可以實際的試試看，就知道我說的是甚麼意思了。 我個人是喜歡用第一個方法， --lab 。
```
$ ionic serve --lab
```
```
$ ionic serve
```
在 ion-icon 中 顏色預設值有下列幾種，呈現出來的效果，我也附上截圖供大家參考一下~
```html
  <ion-icon name="heart" color="bright"></ion-icon>
  <ion-icon name="heart" color="vibrant"></ion-icon>
  <ion-icon name="heart" color="secondary"></ion-icon>
  <ion-icon name="heart" color="danger"></ion-icon>
  <ion-icon name="heart" color="primary"></ion-icon>
```
![heart](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/heart.png "heart")
