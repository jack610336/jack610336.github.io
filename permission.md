---
title: Android 危險權限問題
---

有時候當從手機取資料取不回來的時候，logcat回傳值一值為null，但是我們已經在AndroidMainfest中已經加入權限了

那就表示我們很有可能用到危險權限，所以需要和使用者請求權限!

切勿忘記，不然我們程式可能會無法運作或是崩潰

在這邊我們利用GPS定位來做為範例練習

REQUEST_CODE  用來傳遞至 onRequestPermissionsResult() callback方法使用 (一個自訂義的值)
``` java
private static final int REQUEST= 0;
```

我們在有需要用到權限的地方寫入下面這段，一開始未取得權限，會做什麼事情，都在此處動作(基本上每次開啟app都會進入這段程式碼判斷是否取得權限及後續動作)

```java
int permission = ActivityCompat.checkSelfPermission(this,ACCESS_FINE_LOCATION ) ;

if (permission != PackageManager.PERMISSION_GRANTED ) {
            //未取得權限，向使用者要求允許權限
            ActivityCompat.requestPermissions( this,new String[]{ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION  } , REQUEST  );
} else {
            //已有權限，可進行GPS讀取
            getGPS();
}
```

當跳出提示詢問User是否需要允許權限給App的時，這個時候如果User允許或失敗會發生什麼事情(通常只會安裝完第一次執行App會進入這段，因為如果接受權限後就不會再跑這段，除非User按下拒絕給予權限，那當再次要求權限的時候才會跑進這段程式碼來)

當跳出詢問畫面後，要判斷是否同意或拒絕權限，如果拒絕，記得需要提醒User 按下拒絕後哪些功能是無法使用的。  

```java
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {

        switch (requestCode) {
                case REQUEST  :
                    if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED ) {
                            //已經取得使用者同意後，可在裡面放入要同意權限後做的事情
                            getGPS();
                    } else {
                            //使用者拒絕權限後，提示使用者的彈跳視窗
                            new AlertDialog.Builder(this)
                                    .setMessage("必須允許GPS權限")
                                    .setPositiveButton("OK", null)
                                    .show();
                    }
                    break;
        }    
}
```

當在其中一個activity中取得權限後，其他的activity都可以使用該權限，無需要再和使用者取一次權限

所以簡單來說，當某個權限得到允許後，該app都可使用該權限


## Reference
Request App Permissions : [https://developer.android.com/training/permissions/requesting.html#perm-check](https://developer.android.com/training/permissions/requesting.html#perm-check)   
Permissions Overview : [https://developer.android.com/guide/topics/permissions/overview.html](https://developer.android.com/guide/topics/permissions/overview.html)
