---
layout: post
title:  "[心得筆記] Channel 9 - 使用 TypeScript 駕馭 Web 世界的脫韁野馬： 以 Angular 2 開發框架為例"
date:   2016-07-30 23:05 +0800
categories: ClassReview
---

# 前言
> 閱讀保哥部落格文章 [前端工程的夢幻逸品：Angular 2 開發框架介紹][1]，其中有保哥在 Channel 9 的[演講影片][2]，
以下是觀看線上演講影片的心得整理。

# Angular 2 vs. Angular 1
- 效能改進 (Performance)
    - 偵測速度: 比 ng1 快 10x
    - 渲染速度: 比 ng1 快 5x
    - 範本編譯: 支援 Template 預先編譯載入
    - 更小的 Library Size
    - 支援伺服器渲染機制
- 高生產力 (Productivity)
    - 更簡潔的語法
    - 更強大的開發工具 Angury
    - 移除超過 40+ 個 directives
- 多樣平台 (Versatility)
    - 支援 Browser, Node.js, NativeScript and more...

# Angular 2 開發語言
TypeScript

## Angular 2 應用程式的組成
- App Component: 一個根元件，最上層
- Child Component: 子元件
- Services Component: 服務元件
- Pipe Componet

以元件為中心化，高度模組的組成(OS. 跟 react 概念好像阿，以後 js 都變這樣嗎 @_@

### Angular 2 頁面的組成
一般 ng2 頁面主要組成結構會如下: 
AppComponent + Templates 
HeaderComponet
SiteComponent
Mainomponent

### Angular 2 結構剖析
- Module
- Component
- Template
- Metadata
- Data Binding
- Directive
- Service: 由**服務**集中管理資料與運算邏輯
- Dependency Injection: 由**相依注入**機制管理生命週期

#### 範本 Template
- HTML 版面配置
- HTML 部分片段
- 資料繫結 (Bindings)
- 畫面命令 (Directives)

#### 類別 (Class)
- 建構式 (Constructor)
- 屬性 (Properties)
- 方法 (Methods)

#### 中繼資料 (Metadata)
- 裝飾器 (Decorator) <- ES7 的功能
     - 針對類別
     - 針對屬性
     - 針對方法
     - 針對參數

# Start live demo

## 手動建立基礎開發環境

1. 應用程式資料夾
2. tsconfig.json
3. package.json
4. typings.json
5. libraries & typings
6. index.html
7. main.ts (bootstrapper)
8. .gitignore & sourcecode manage
9. developer tool

##### 以上零零總總制式的建立以及設定的東西，使用 **Angular CLI** 建立專案範本來自動完成。

使用 `$ npm start` 啟動 webpacke 自動 bundle 等等。

#### 裝飾器 (Decorator)
實作用 @Component 作為宣告語法，其實就跟 C# 的 Attribute 是一樣的東西。

### 建立 derective & component

### 建立 Compnent 和 Component 之間的連結
使用 import 方式來載入

### 建立注入遠端資料 Component

`import {Http, Response} from '@angular/http'`

在 `constructor` 注入 Http, 建立 angular component 的生命週期 functions, 建立 `ngOnInit()` 來載入遠端 json 資料。  

在 HTML 元素上使用 `*ngFor="let post of posts` 用來 repeat 迴圈塞值。  

用 Properties Binding 的方法 `[xxx]="post.url"`  

輸出 html tag, `[innerHtml]="post.summary"`

### two way binding 
將值從外層傳到內層，`<input type="text" [(ngModel)]="keyword" ...>`，然後再 component 中，使用 keyword= xxx 就可以抓到了，輸出直接用 `{{keyword}}` 就可以輸出了。

```
<posts 
   [search]="keyword"
></posts>
```

連回 PostsComponent 宣告一個 search property 再透過 Decorator & Metadata 來宣告讓外面可以取得。

### 過濾的動作
寫 `ngOnChanges()` 去觸發 component 的事件，在套上條件後，重新調用 api，就可以取得條件後的資料，再重新綁定。

### 介紹 typeScript 的 interface
import components，用 typescript 的 interface 來發現未實現的 interface 方法。

### 設計 interface 來解決 service 回傳資料型別問題
建立好 interface 結構，在 component import interface, 就可以將 service 回傳的 object 給上型別。

## 結尾
演講最後回顧 angular2 的特性，在 slide 中快速帶過。
投影片[載點][3]


[1]: http://blog.miniasp.com/post/2016/07/26/Introduction-to-Angular-2.aspx
[2]: https://channel9.msdn.com/Events/AzureDevDay/2016/A02?ocid=player
[3]: https://onedrive.live.com/redir?resid=5F91F4CB09EC294C!2196&authkey=!AEDOwwN29zw8Ejc&ithint=file%2cpdf