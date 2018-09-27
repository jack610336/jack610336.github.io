最簡單的跳頁要怎麼做呢?
其實很簡單 navigation 元件
大家可以把畫面想成一個堆疊的array，只有當使用者在使用那一頁的時候
會顯示出當下的畫面，所以會將需要的那一頁，push出來到最前頁。

所以這個時候就很簡單的可以理解，我們可以先創一個新的Page
當然，在創立新頁面的時候，我們需要在app.module.ts裡面 加入我們的頁面。

```ts
@NgModule({
  declarations: [
    MyApp,
    HomePage,
    UsersPage   // 這是我們新增的頁面
  ],
  imports: [
    BrowserModule,
    IonicModule.forRoot(MyApp)
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    HomePage,
    UsersPage    // 這是我們新增的頁面
  ],
  providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
})
```
然後在HomePage 加入一個 ion-button
```html
<!--Home.html-->
<button ion-button (click)="onGotoUsers()"> Users </button>
```
```Typescript
//home.ts
onGotoUsers() {
    //push的原因就是因為我們要把它push到最前頁的意思，所以當使用push時候，我們會跳至UserPage頁面
    this.navCtrl.push(UsersPage)

  }

```

當在使用Tab的時候，可以透過selectedIndex 來控制載進畫面的時候，預設要選哪一個tab
```html
      <ion-tabs [selectedIndex]="1">   select the default tab, start from 0
        <ion-tab [root]="favoritesPage" tabTitle="Favorites" tabIcon="star"></ion-tab>
        <ion-tab [root]="libraryPage" tabTitle="Library" tabIcon="book"></ion-tab>
      </ion-tabs>
```



左滑刪除項目，在ionic中有個非常簡單的元件，<ion-item-sliding> 可以直接做出一個左滑後
的側邊項目，搭配<ion-item-options>使用，這個是用來做左滑後的東西，可以放入button 等等元件

例如 :
```html
<ion-list>
    <ion-item-sliding *ngFor="let quote of quotes">
      <ion-item (click)="onViewQuote(quote)">
        <h2> {{quote.person}}</h2>
        <p>{{quote.text}}</p>
      </ion-item>
      <ion-item-options>
        <button ion-button color="danger" (click)="onRemoveFromFavorites(quote)">
          <ion-icon name="trash"></ion-icon>
          Delete
        </button>
      </ion-item-options>
    </ion-item-sliding>
  </ion-list>
```


ionic中要將數字限定小數幾位，在angular 中有pipe 功能可以使用，如下:
```Typescript
{{test | number:'3.1-5'}}
 // 意思是小數點前面有三位數，小數點後最少一位，最多五位數字。
```
