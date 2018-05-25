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
