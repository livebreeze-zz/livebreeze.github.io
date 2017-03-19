---
layout: post
title:  "[心得筆記] Angular 2 開發實戰：新手入門篇 第一階段 (保哥線上課程)"
date:   2016-07-27 23:05 +0800
categories: ClassReview
---


# Outline
- Angular 2 相關工具
- TypeScript與相關工具
- TypeScript 與 ES6 語言特性


# vs code
- Free
- 開放原始碼
- 跨平台 (Linux, OSX, Windows)
- Extensions
- 適合用來偵錯 Web & Cloud
- 開發工具是用 TypeScript & Electron 打造而成

## 介紹 visual studio code
- 側邊欄介紹 (檔案總管, 搜尋, git 版控, 偵錯,  擴充套件)
- 狀態列 (編輯器畫面最下方的藍色bar，針對目前開啟的檔案，顯示當前編輯資訊)


>Tips:  

- 檔案總管
    - Ctrl + Click 開新的編輯視窗
    - Ctrl + B 隱藏側邊攔
- 編輯室窗
    - Ctrl + . 智慧標籤

# 簡介 nodejs & npm
npm 建議不要用指令搜尋，建議用網站搜尋
因為比較快，快蠻多的

`$ ng`  
`$ tsc`  
可以用文件編輯器打開，會發現就是批次檔, 使用 nodejs 去執行的 node 文件

`$ npm install lodash --save`  
`--save` 的作用就是下載套件放到當前目錄 node_modules 中


## 簡介 gulp
雖然在 ng2 已經用到比較少，不過還是前端工作流程還是好用。  
編寫一些腳本，簡化一些前端工作。

# 簡介 webpack
在 ng2 非常重要，是一個模組相依性的工具，目前 angular 官方，已經將 webpack 列入官方模組化管理的工具。

- 模組包括: html, js, coffe, css, less, png, webfonts, ...
- 透過**靜態的檔案**來取代**相依模組**

空純文字的 ng2 會發出 341 個 request，722KB 的流量，用 webpack 後會簡化到不到 10 個 request, 100KB 左右流量。

---

# 認識 TYPESCRIPT 與相關工具

> 一個能**在開發時期**宣告**型別**的 JavaScript **超集合**，可以被**編譯**成 JavaScript 程式碼

TypeScript 包含所有 es 版本，再加上一些很好用的語法糖。並且解決 js 不好維護，不適用大型專案上變的缺點。

ts 語言特性:

- 支援靜態型別: 邊義器檢查
- 支援介面型別: 擴充 js 缺少的語言特性
- 型別自動推導: 自動判斷物件型別，像是 c# 的 var 自動推導
- 先進語言特性: 可支援js最新規格(es6)

## 使用 ts 亮點

- 完整有效的 js 語法，100% 相容
- 可呼叫現有的 js libary
- 強大的工具資源 (ex. vs code)，大幅提高開發生產力
- 先進語法都能用

## 使用 tsc 命令列工具

- 初始化 tsconfig.json 設定檔
- 編譯 tsc   
等等...   

>tip:  
ng2 已經包括了 tsc 的命令工具了，所以了解原理即可，已幾乎用不到 tsc 命令。

VSCode 隱藏一些自動產生的檔案，不顯示在 solution bar

參考網路資源:  
[VS Code 檔案顯示設定](https://jeffwu85182.github.io/2016/07/21/vscode-file-display/)

### 認識 Typings 工具
- 簡介
    -  Typings 將常見的 JS 框架/函式庫(外部模組)的**模組定義檔**(*.d.ts)封裝進一個被完善定義的命名空間。
    
> Tips
`$ typings init`  
`$ typings install dt~jquery --global --save`  
就會在專案裡面建立模組定義檔，而且定義檔只有 interface, typescript 編譯完之後，就會將 interface 編譯成空的，就不會將定義檔編譯進 js 檔案了。有了定義檔，大大改善了 js 打錯字的問題。


### ES6 變數與常數
- var
- let
- const

const 如果為物件，其底下的屬性是可以改的。
重提注意 js hosting 特性，

#### let
可多研究 let 的作用域影響，let 同一個區域範圍內，不允許重複宣告。  

> 以 for 迴圈搭配 setTimeout 印出 i 值做範例
迴圈計量變數用 var 與 let 的差別，for 迴圈初始化的 i 變數，使用 var 宣告的話會因為提升，印出最後一個值，但 let 宣告的話，在每一個迴圈內是獨立的變數 i, 不會受其他迴圈影響。


#### 字串型別  

*es6 語法*  **backquote 反引號**用法

```
let color: string = "blue";
color = 'red';

let fullName = `Will`;
let age = 37
let sentence = ` Hello, my name is ${ fullName }.

I'll be ${ age +1 } years old next month.`;

console.log(sentence);
```

---

# TypeScript

#### TypeScript 練習
上 [typescript 官網](http://www.typescriptlang.org/play/index.html) 練習 TypeScript。

*ts 語法*   

- Array(簡單陣列型別)
- Tuple(複合型別陣列型別) - 陣列裡面可規定不同的型別陣列
- Enum (列舉)
- any (任意型別)
- Object (物件型別): 一般不會這樣寫，因為比較難看
- void: 通常用在 function 回傳值，不過 typescript 自己會自動判斷 return 值，所以也可以不寫。

#### 型別轉換 Type assertions


### 介面 Interface  
interface 單純只用型別檢查，因為轉成 js 就會不見了。  

方法傳入的參數，如果是直接在方法裡面傳入**物件實字表示法**，ts 會不允許傳入多餘參數，  
但如果是將物件宣告為**變數**帶入，就可以通過檢查，可傳入帶有多餘參數的物件;   

官方說明是，通過**實字表示法**這樣傳遞不一樣數量的參數，通常是打錯了，而宣告為變數傳入多餘的參數，則通常是擴增，所以會有這樣的驗證設計差別。


### 類別 class

> tip:   

- 類別的裡面的方法，不需要 function 表示式，直接打方法名稱就可以了。
- get set 存取子  
[refactorix](https://marketplace.visualstudio.com/items?itemName=krizzdewizz.refactorix) 使用方法      
`>X: property to get set`  

**抽象類別**

### 泛型 Generics
ts 會有自動型別推導，所以可以從傳入的參數自動推導出泛型的型別，就可以不用再使用方法的時候指定。

- 泛型函式
- 泛型介面
- 泛型類別

## es2015 / ts 模組化技術
- module
- export
- import

### 裝飾器 Decorators
@ 開頭，很像 c# 的 attribute  
目前 ts 式實驗性的功能，預設不啟用，不過 ng2 已經在設定在 tsconfig.json 裡面了。

### 符號 Symbols
es2015 新的原始型別

### 迭代器 Iterators
- Array, Map, Set, String, Int32Array, Unit32Array  預設有內建迭代器，有迭代器就可以搭配 for..of 的語法
- for..in vs. for..of 差別  

簡單的說，就很像 c# 的 for 和 foreach 的差別。  
他就是 C# 實作 IEnurable 的做法, 這就是語言的迭代器。  
for..of 是 generation 決定產生的，保哥用 window[Symbol.iterator] 舉例自建出一個 for..of。  

Symbol + Generater + Iterators 整合起來就是 for..of  


### 展開運算子 Spread operator
- myFunction(...args);  
  就是把陣列換成逗號分隔成參數傳入

```
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
```

- 傳統 js 解法不用迴圈合併的方法  
  `Array.prototype.push.apply(arr1, arr2);`
- 使用展開運算子  
  `arr1.push(...arr2);`

更彈性的函式參數傳入

- function myFunction(v, w, x, y z) {} 
- var args = [0, 1];
- myFunction(-1, ...args, 2, ...[3]);  

```
var a = [1, 2, 3]
var b = [4, 5]
var c = [...a, ...b]
// c 就是一個併了 a&b 的新陣列
```

Immutable.js 舉例

```
var a = [1, 2, 3]
var b = 4;

// 如何產生一個全新的陣列

var c = a;
c.push(4);
// 這樣 c 參考 a, 會有參考問題

// 解決方法
var b = [...a, 4];
```

> Q. 哪些東西可以用**展開運算子 Spread operator**?  
基本原則: 只要有實作迭代器(Iterators) 就可以使用展開運算子。  
必須能有 for..of 才有辦法實作出迭代器。

*ES6 新特性*  
**其餘參數(Rest parameters)**

```
// 以前 js 的抓法
var args = Array.prototype.slice.call(arguments, f.length);`

// 使用展開運算子的抓法
function f(a, b, ...args){
    return args;
}
```

## Q&A:
1. 產生 get set 的 **vs code** extension ?  
[refactorix](https://marketplace.visualstudio.com/items?itemName=krizzdewizz.refactorix): 重構 typescript 的工具。

2.  有 npm 還需要 bower 嗎?  
保哥: 建議是已經不需要用了。
