Google Maps Android API








再使用google map 時
要再gradle 裡面新增 //可能版本不一樣，但是必須要加入
``` xml
 android.gms:play-services:v7+
```


再進到android manifestest.xml 加入下列語法

``` xml
<meta-data
  android:name = "com.google.gms.version" // 跟app說 gms版本是多少
  android:value ="@integer/google_play_services_version"/>
}
```


最後再加入權限，依據不同狀況新增不同的權限。

當我們開啟一個地圖服務的App時候
他的啟動順序及生命週期如下圖



我們在編輯Manifest 做一個新的地圖App的時候，需要做的三大步驟

1. 開啟一個新的XML(介面)
1. 編輯我們的gradle檔案(要加入gms 服務)
2. 最後在編輯 Android.manifest檔案，這裡需要添加四個項目
  * Services
  * OpenGL
  * API Key
  * 使用權限

















## Reference
 Udacity - Add Google Maps to your Android App
