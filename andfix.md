andfix

平常我們在更新Android App的時候，都只能透過Google Play給使用者更新
如果今天我們臨時有一個突發的Bug，想要即時更新，是不是只能透過Google Play呢?
這樣使用者可能會想，我才剛下載安裝完，結果馬上又要在更新一次?乾脆直接移除App好了
這樣也許會增加使用者的困擾及對此App的信心。
這時候我們就想說能不能透過即時更新的方式，讓App直接連網路更新呢!
這個很多大型公司或是銀行的App都有這種需求，所以我們今天介紹的一個是由阿里巴巴開發的一個套件
AndFix全名為Android hot-fix，其實有很多公司有開放這樣子的套件和架構
雖然這個套件，目前好像已經沒有在更新了，阿里巴巴他們似乎開了一個新的專案，來製作熱更新的部分。
不過這個套件對於中小型專案，小的hot-fix來說，還是很實用的。



AndFix有些限制
* 不能新增字串和新的class
* 無法修復application的 onCreate方法
* 無法修改一般class 的建構值
* 目前版本支援度為 Android 2.3 ~ Android 7.0 (API 27 無法成功使用，筆者實際測試過)

在AndFix 官方說明中有提到安全性問題，為了確保APP更新的patch是我們發行的，不是其他人任意修改的patch，建議我們在更新之前要先驗證patch的金鑰簽名和指紋簽名。

```txt
Security
The following is important but out of AndFix's range.

verify the signature of patch file
verify the fingerprint of optimize file
```
https://github.com/alibaba/AndFix/blob/master/images/principle.png
看一下AndFix的架構圖，他其實是替換掉原本方法，

這篇就帶大家手把手從零開始教學

首先我們在 gradle dependency 中加入下面這段，就可以開始使用AndFix了

``` java
dependencies {
	compile 'com.alipay.euler:andfix:0.5.0@aar'
}
```

***
* 初始化     
首先一般初始化都在是application，先創建一個class繼承application。
然後再來時做AndFix的必要方法，下列是完整程式碼

```java
package com.jack.andfix;

import android.app.Application;
import android.os.Environment;
import android.util.Log;

import com.alipay.euler.andfix.patch.PatchManager;

import java.io.IOException;

/**
 * Created by Jack_Wang on 2018/4/25.
 */

public class MainApp extends Application {

    private static final String APATCH_PATCH = "/hotfix/";//存放patch的資料夾
    private static final String Type = ".apatch";//patch檔案類型
    private static final String TAG = "TAG";

    private PatchManager mPatchManager;

    @Override
    public void onCreate() {
        super.onCreate();
        mPatchManager = new PatchManager(this); //初始化PatchManager
        mPatchManager.init("2.0");//當前App版本，patch只能用在相同的App版本
        Log.e(TAG, "inited." );

        //load patch
        mPatchManager.loadPatch();//讀取所有patch
        Log.e(TAG, "loaded");

        try {

            String patchFileString = Environment.getExternalStorageDirectory().getAbsolutePath()
                        + APATCH_PATCH ;
            mPatchManager.addPatch(patchFileString + "1" + Type); //更新App
            mPatchManager.addPatch(patchFileString + "2" + Type);
            mPatchManager.addPatch(patchFileString + "3" + Type);

            Log.e(TAG, "added" );
            mPatchManager.removeAllPatch(); //移除patch，不是刪除全部patch
        } catch (IOException e) {
            Log.e(TAG, " IOException");
        }
    }
}
```

***
* 接下來我們在androidManifests加入我們需要的權限及關連  
加入權限
```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
```
關聯我們自己建立的application class
```xml
<application
        android:name=".MainApp"
      .....
```
下列為完整的程式碼 :

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.jack.andfix">

    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />

    <application
        android:name=".MainApp"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

***
新增完後，我們可以開始測試，hotfix功能
我們直接改hello world的字詞來做測試。

```java
    private TextView mTvTest;
    private String ShowText;
@Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       checkPermission();//這個為自己實作的權限設計，Android 6.0 有危險權限的關係。
       mTvTest = findViewById(R.id.tv_test);
   }

   public void click(View view) {
       ShowText = "V2_2_patch"; //我們就更改中間的showText值來作為patch的不同
       mTvTest.setText(ShowText);
       Toast.makeText(this, ShowText, Toast.LENGTH_SHORT).show();
   }
```

官網的github中有提供一個檔案來做為檢查兩個apk檔案的差異，進而製作出patch來的工具
https://github.com/alibaba/AndFix/raw/master/tools/apkpatch-1.0.3.zip
解壓縮後放在同一個資料夾，要如何使用呢，windows系統下使用的是.bat檔案，linux底下適用.sh檔案，然後因為我們等下回輸出一個patch檔案，所以在這邊我先建立一個資料夾，等等將檔案輸出至新建的資料夾中

在開始之前，我們需要先用android studio 這個apk做一份金鑰，再放進相同的資料夾裡。
再將我們的apk檔案也都放進資料夾中，一個為舊版(有bug)，一個為新版(修正過後的app)

在windows下，兩種方法
* 按下shift + 滑鼠右鍵，可以看到一個選項為在此處打開一個命令窗口。
* 打開命令提示字元，將目錄切換到目前的資料夾即可。    

在cmd畫面輸入下方指令

```txt
apkpatch.bat -f new.apk -t old.apk -o output -k debug.jks -p debug_password -a androiddebugkey -e androiddebugkey_password
```
for example

outputfolder 是剛剛創的新資料夾名稱，這樣apkpatch會在分析完後，將檔案創建於這個資料夾中。
```txt
apkpatch.bat -f new.apk -t old.apk -o outputfolder -k debug.jks -p 123456 -a androidKey -e 123456
```

分析完後，我們可以在新的資料夾中，看到一個.apatch檔案的patch，由於我們目前是測試，所以我們先安裝舊版的apk，打開執行後，看到確定是舊版的APP，請先關掉它，後台也要清掉。
