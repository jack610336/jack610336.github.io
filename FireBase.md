---
title: Android 使用 FireBase 註冊及教學
---

<html>
  <head>
  <!-- Favicon and touch icons -->
<link type="image/x-icon" href="/img/favicon.ico" rel="icon" />
<link type="image/x-icon" href="/img/favicon.ico" rel="shortcut icon" />
<link type="image/x-icon" href="/img/favicon.ico" rel="bookmark" />

<!-- Favicon for Chrome -->
<link rel="icon" type="image/png" href="/img/bookicon.png" />

<!-- Favicon for Safari Web Clips-->
<link rel="apple-touch-icon-precomposed" href="/img/bookicon.png" />
<link rel='apple-touch-icon-precomposed' sizes="76x76" href="/img/bookicon.png" />
<link rel='apple-touch-icon-precomposed' sizes="114x114" href="/img/bookicon.png" />
<link rel='apple-touch-icon-precomposed' sizes="120x120" href="/img/bookicon.png" />
<link rel='apple-touch-icon-precomposed' sizes="144x144" href="/img/bookicon.png" />
<link rel='apple-touch-icon-precomposed' sizes="152x152" href="/img/bookicon.png" />

<!-- Favicon for Win10 Edge -->
<meta name="msapplication-TileImage" content="/img/bookicon.png">
<meta name="msapplication-TileColor" content="#226533">



  </head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
  <style>
      .w3-theme {color:#fff !important;background-color:rgb(90, 180, 207) !important}
      .w3-btn {background-color:rgb(90, 180, 207);margin-bottom:4px}
      .w3-code{border-left:4px solid rgb(90, 180, 207)}
      .myMenu {margin-bottom:150px}
  </style>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</html>

# Android 使用 FireBase 註冊及教學

#### 導入FireBase

首先我們需要有Firebase的帳號，所以我們要先到官網辦一個帳號。  

[Firebase 官網](https://firebase.google.com/)  

登入之後，點選GET STARTED，我們就可以進入下一步了      

![FirebaseLogin](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/firebaseLogin.png "FirebaseLogin")

進入Firebase console的畫面，目前我是有兩個專案，不過我們新開一個專案來做測試看看。   

![FirebaseConsole](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/firebaseConsole.png "FirebaseConsole")

按下新增專案後，需要給他一個專案名稱和所在位置的國家，ID部分我們不需去改變，他是firebase自動幫我們產生的一個唯一ID，確認好後我們就建立新專案了!

![bmitest](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/bmitest.png "bmitest")

我們可以在右邊看到有Project Overview和四大分類的項目

在Project Overview中 我們可以將Android App、iOS App或網路程式加入firebase中。    
而四個分類的細節分別如下 :

* DEVELOP - 帳號驗證、資料庫、Hosting...
* STABILITY - 效能分析、當機報告、測試APP...
* ANALYTICS - App 分析、點擊量分析、下載群眾區域...
* GROW - 預測功能、雲端推播(FCM)、AdMod...

![firebaseFirstLogin](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/firebaseFirstLogin.png "firebaseFirstLogin")

接下來我們按下將Firebase加入Android程式中，會需要我們註冊應用程式，只需要依照需求填寫套件名稱即可，SHA-1憑證可以在此步驟先完成，有做此步驟的App才可使用Google登入或電話認證功能。

![addFirebaseToProject](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/addFirebaseToProject.png "addFirebaseToProject")

開啟我們的專案，右方有一個Gradle的側頁面，開啟後在Task中找到signingReport，點擊兩下執行檔案，這時候我們在開啟右下角的Gradle Console，就可以看到我們的SHA-1憑證，將其複製下來貼上即可註冊應用程式至Firebase中

![signingReport](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/signingReport.png "signingReport")

第二步，我們就照著圖片所教的，將google-services.json放進Android Studio中的專案

![addFirebaseToProject2](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/addFirebaseToProject2.png "addFirebaseToProject2")

最後一個步驟，根據Firebase的說明，添加Gradle中的設定

在project的build.gradle加入下列相依性

``` java
buildscript {
  dependencies {
    // Add this line
    classpath 'com.google.gms:google-services:3.1.0'
  }
}
```

在app的build.gradle加入下列相依性，請注意，這行必須加在最後一行，如果沒有放在最後一行在Sync的時候會有錯誤產生

``` java
// Add to the bottom of the file
apply plugin: 'com.google.gms.google-services'
```

![addFirebaseToProject3](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/addFirebaseToProject3.png "addFirebaseToProject3")

將上述步驟都完成後，我們就將App加入Firebase了    

![finished](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/finished.png "finished")

接下來我們就會開始介紹如何在Android Studio中啟用Firebase的功能    
