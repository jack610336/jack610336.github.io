---
title: FireBase Database 功能，將資料寫入雲端資料庫中
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


# FireBase Database 功能，將資料寫入雲端資料庫中

在上一篇我們完成了Firebase 的註冊及將我們的應用程式加入Firebase中，在這篇文章中我們會講到如何將資料讀寫進入Firebase的雲端資料庫中，只需要三個步驟即可完成簡單的讀寫功能    

* 在 Android Studio 連接 Firebase
* 在 Gradle 中加入相依性
* 實作寫入及讀出資料庫

#### 在 Android Studio 連接 Firebase

在 Android Studio 中，非常容易就可以連接 Firebase，多虧了 Google 的強大，把許多功能整合進來。   
我們可以在工具列中的 Tools/Firebase 開啟 Firebase 助手，開啟後可以看到有許多的Firebase功能，分析、雲端訊息、認證...等等，這些都很簡單的整合在 Android Studio 中，只需要做幾個步驟就能使用了!    

![FirebaseAss](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/FirebaseAss.png "FirebaseAss")

此篇文章主要用到資料庫的部分，所以我們先點擊 Realtime Database 的部分進行設定，進去之後可以看到有步驟教學，那我們先從第一步 Connect 做起，將自己目前的 Project 和上一篇開啟的 Firebase 上的專案做連接，就可以看到圖片中的 Conneted 表示已連接   

![connectFirebase](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/connectFirebase.png "connectFirebase")

連接完成後，我們需要將 Realtime Database 加至我們的 App 中，所以案下去後，系統會提示我們目前缺少那些相依性，然後詢問是否要幫你自動加入並 Sync，當相依性添加完成後，就很簡單的完成了連接的動作了，接下來我們需要的是在 Firebase 上的資料庫進行一下簡易的設定，就可以回到 Project 準備開始寫程式了

![addDatabase](https://raw.githubusercontent.com/jack610336/jack610336.github.io/master/img/addDatabase.png "addDatabase")
