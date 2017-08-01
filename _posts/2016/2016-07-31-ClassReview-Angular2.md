---
layout: post
title:  "[心得筆記] Angular 2 開發實戰：新手入門 (保哥課程)"
date:   2016-07-31 22:05 +0800
categories: ClassNote
author: Sean.C
tag: [ClassNote, Javascript, Angular2]
bgimgurl: https://raw.githubusercontent.com/livebreeze/BlogImages/e5ae2b0d2d34430043ac20879b52243eb0067a9e/Images2016/20160803_PostBGImg.jpg
---

## 前言
這篇是今天上完 [《台中》Angular 2 開發實戰：新手入門篇][1] 的課後筆記與心得。  

課程主要內容:

> - 學習 Angular 2 之前的準備工作 (線上進行)
> - 體驗 Angular 2 開發流程

上課前有兩堂的 zoom 會議課程，   
第一堂是保哥的小助手介紹與安裝開發環境，包括 vs code, nodejs, npm 一些相關套件的基本的安裝與操作等等。  
第二堂是保哥介紹 **Angular 2 相關工具**, **TypeScript與相關工具** 與 **TypeScript 與 ES6 語言特性**，可以參考前兩天的[筆記][2]。

另外保哥近日也有新增一篇關於 angular2 的介紹文章 - [前端工程的夢幻逸品：Angular 2 開發框架介紹][3]，裏頭說明 angular2 的特性。  
此外文章中有 typeScript 以 angulr2 為範例的 [chanel 9 演講影片][4]，保哥在 1 小時內 demo 如何使用 angulr 2 實現 blog 網站。  
我這邊昨天看完有寫一點[筆記][5]，而今天上課的課程感覺有近 8 成和影片演講內容是差不多的，上課是多了讓大家實戰練習與一些小細節的說明。  
因此今天的心得筆記，就專注在一些實戰上面的流程與小技巧。

---

## Demo 開始

## 遇到問題
前端開發經常麻煩就是遇到一些執行環境的問題，雖然說 mac 的 OSX 相較於 window 已經比較沒什麼問題，不過今天還是遇到了狀況。  
因為手癢搬了一下檔案的目錄位置，結果 server rebuild 卻拋出錯誤，其中關鍵字是 .DS_Store，這東西是個 OSX 的應該類似 cache 或者檔案索引的隱藏目錄，在網路上有查到相關的解法如下

```
// 禁止.DS_store生成：
$ defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE
// 刪除已存在的.DS_Store
$ sudo find . -name ".DS_Store" -depth -exec rm {} \;

// 恢復.DS_store生成：
$ defaults delete com.apple.desktopservices DSDontWriteNetworkStores
```

## 練習專案
上課練習的專案檔案放置[我的 github][6]，可以從 Commit 紀錄看到練習過程，另外保哥今天的 demo 專案與步驟也有放上 [github][7]。

## Angular-CLI
在第一堂上課有安裝一個 npm 套件 [Angular-CLI](https://cli.angular.io/)，首先就用 cli 初始化 demo 專案。  

### 初始化建立專案

```
$ ng init
```

經過一段時間等待後，乾淨的 angulr2 專案範本就建立好了。  

### 建立新 component
接下來使用新增 component 指令 `$ ng g c xxx` 來新增 component，固定會產生相關的4+1個文件檔案 (其中 xxx 是 component 名稱):

- index.ts
- xxx.component.ts
- xxx.component.html
- xxx.component.css
- xxx.spec.ts  
    (這是單元測試檔案，如果僅是 demo 不用單元測試可以不用理會他)

練習將保哥 blog 靜態網站的 source 搬進 component 裡面去實作，增加 template 到 .html 檔案，增加綁定變數到 .ts 檔案。
接下來再上層 app.compoent 去 import 新增的 compoent 模組

```
import { HeaderComponent } from './header'; // 預設進入點會找資料夾中的 index.ts
```   

> Tip

import 的 from 指定路徑設定不能加副檔名，因為 typescript 會利用 systems 來管理模組，自動加上副檔名，如果自己加了會報錯。另外 systems js 將會被 **webpack** 所取代，angular 官方已確定將導入 webpack 作為模組管理。


### 啟動 Angular 2 開發伺服器
執行以下指令，會啟動 angular2 開發伺服器，而且當專案有存檔時， Angular CLI 會自動 rebuild 並且 browser sync 自動頁面刷新。

```
$ ng serve
```

> Tip: angular 執行發生錯誤可以捕捉錯誤的地方

- `$ ns serve` 在 cmd 會秀出錯誤訊息
- 開發工具 vs code 會飄線表示錯誤
- Chrome develop tool 的 console 也會有錯誤訊息

Angular2 的錯誤訊息機制，是使用 [Zone][8] 來實現的，因此相較於 Angular1 & React js 親民很多。


## 4 種資料繫結方法 (Binding syntax)

### 內嵌繫結 (interpolation)
*雙大括號包起來

``` 
\{\{ property \}\}
```


### 屬性繫結 (Property Binding)
```
[property]="statement"
```

### 事件繫結 (Event Binding)
```
(event)="someMethod($event)
```

- 注意 `$event` 是 ng2 固定用來傳遞觸發事件的參數固定名稱。

### 雙向繫結 (Two-way Binding)
```
[(ngModel)]="property"
```

## 3 種 angular 指令 (Directives)

### 元件型指令
預設**元件**(Component) 就是含有樣板的指令(最常見)

### 屬性型指令
用來修改元素的外觀或行為，例如內建的 `ngStle`, `ngClass`。

### 結構型指令
用來透過新增和刪除 DOM 元素來改變 DOM 結構，例如內建的 `ngIF`, `ngFor` 或 `ngSwitch`。

## 範本參考變數 (Template reference variables)
在 template 中任意 HMLT tag 可以套用 #name 語法，就可以透過此 name 變數將 DOM 元素往 ng 方法傳遞。

## 元件的輸入輸出
在 Component 之間的值互相傳遞的方法，就是透過 `@Input()` 與 `@Output()` 來實現，使用時要 import 內建的 Input, Output 元件。  
另外值得注意的是，因為 Component 之間的傳遞，在專案日趨肥大而複雜後， in/output 會變得難以觀察與維護，因此課程最後會介紹一個建立 angualr service 的東西，用來解決傳遞值得問題。

### 傳入屬性
在 component 裡面的屬性套上 `@Input()` 後，就可以在*外層元件*用**屬性繫結**傳入資料。

```
@Input()
myProperty;
```

### 傳出事件
在 component 裡面的事件套上 `@Output()` 後, 在*外層元件*使用**事件繫結**來接收傳出的資料。  
注意使用 `$event` 來接收子元件傳出的資料。

```
@Output()
myEvent = new EventEmitter();
this.myEvent.emit(data);
```

## 指令元件的主要生命週期 Hooks
- ngOnInit
- ngOnChanges
- ngDoCheck
- ngOnDestroy

## 使用 Pipes
這東西很像 ng1 的 filter，不過叫做 pipes, 用法就是一根管子 `value | pipe`，沒錯!就是 ng1 的 filter 寫法。

### Angualr2 內建的 Pipes 元件
- uppercase, lowercase
- date
- number, decimal, percent, currency
- json, slice

### Angular2 沒有內建 FilterPipe 與 OrderByPipe
因為在 ng1 這兩個經常被濫用，導致效能低落，另外因為 JS 沒有**傳值**的特性，所以導致經常有 bug 出現，  
那要怎樣做到過濾功能呢? 自己刻，其實也不難，簡單方法就是結合**事件綁定**，然後將 value 利用 es5 的 .filter 語法過濾資料後，再回傳即可。

# Angular2 相依注入

## 建立服務元件
前面在*元件的輸入輸出*有提到在複雜的專案下，過於複雜的 component in/output 傳遞，會導致可維護性變差，所以這邊可以利用**服務元件**的方式，來從外層注入**值**。
另外要注意在 main.ts 全域注入服務的注入器是獨體模式(Singleton)，也就是剛執行建立的第一份實例化物件，將能給所有 component 使用，達到各 component 共用的目的，但如果又在內層另外注入，則會另外產生新的實例化物件，將可能導致 component 無法從 sevice 取值。

## 使用 HTTP 服務元件
最後因為時間的關係，這段保哥講的比較快，可以參考官方的 [HTTP CLIENT][9] 來實作練習。

## 相關連結
- [Angular2 官網](https://angular.io/)
- [Angular2 簡體中文](https://angular.cn/)(官方認可)
- [Angular2 風格指南](https://angular.io/styleguide)(官方版)
- [Angualr2 學習資源](https://angular.io/resources/)(官方版)
- [Angular2 學習資源](https://github.com/timjacobi/angular2-education)(Github社群版)
- [ng-conf 2016](https://www.youtube.com/playlist?list=PLOETEcp3DkCq788xapkP_OU-78jhTf68j)(YouTube)
- [Rangle's Angular 2 Training Book](http://angular-2-training-book.rangle.io/)

- [Angular 2 Fundamentals](http://courses.angularclass.com/courses/angular-2-fundamentals)(免費 ng2 課程)

- [TypeScirpt](http://www.typescriptlang.org/)
- [TypeScript Handbook](https://github.com/zhongsp/TypeScript)(中文版)

- [Angular Augury](https://augury.angular.io/)

- [A curated list of helpful material to start learning Angular 2](https://github.com/timjacobi/angular2-education)


[1]: http://www.accupass.com/go/DCT_105015
[2]: {% post_url 2016/2016-07-27-ClassReview-Angular2-DevGetStartedClass %}
[3]: http://blog.miniasp.com/post/2016/07/26/Introduction-to-Angular-2.aspx
[4]: https://channel9.msdn.com/Events/AzureDevDay/2016/A02?ocid=player
[5]: {% post_url 2016/2016-07-30-Ch9Class_UseTypeScriptToDevelopAngular2 %}
[6]: https://github.com/livebreeze/Angular2Demo
[7]: https://github.com/miniasp/ng2demo-0731
[8]: https://angular.io/docs/ts/latest/glossary.html#!#zone
[9]: https://angular.io/docs/ts/latest/guide/server-communication.html

