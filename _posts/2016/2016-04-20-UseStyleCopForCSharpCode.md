---
layout: post
title:  "Review - 保哥線上講堂：利用 StyleCop 撰寫一致的 C# 程式碼風格"
date:   2016-04-20 23:59 +0800
categories: ClassNote
---

去年無意間翻找保哥開的課程，發現有一堂線上課程，是關於定義團隊 C# 撰寫風格的 StyleCop，剛好對於 StyleCop 有興趣，又懶得翻閱英文文件，當然是直接上課最快拉!  
而且線上課程想什麼時候學，在那裡學，想學幾遍都可以，所以秒速刷卡就開始零時差零距離開始上課了 XD

# 課程介紹

[《保哥線上講堂》利用 StyleCop 撰寫一致的 C# 程式碼風格 (線上課程)][1]

> 在軟體開發團隊裡通常會想要求一致的程式碼撰寫風格，公司雖然會訂定 Coding Style 要大家遵循，文件寫了一堆，那又如何？公司裡是是誰要來檢查呢？人工檢查也太不切實際了點！本次講座 Will 保哥將分享如何透過 Visual Studio 的 StyleCop 擴充套件做到全自動的程式碼撰寫風格檢查，讓每個人都不用看規範文件，透過工具用最無腦的方式自動幫你做好到程式碼風格檢查。

#### 預期效益:

- 了解 StyleCop 的設計概念
- 了解 StyleCop 安裝與使用
- 了解 StyleCop 的規則如何定義
- 了解 StyleCop 在實務上如何應用
- 了解 StyleCop 如何適用團隊運作
- 了解 StyleCop 如何跟 MSBuild 組建流程整合

### 課程簡報
[(slideshare) 利用 StyleCop 撰寫一致的 c# 程式碼風格](http://www.slideshare.net/WillHuangTW/stylecop)

# 上課筆記
SyleCop 主要分析規則 (撰寫程式碼方面的規範)，總共有七大類，共165條規則。

### 安裝方法
到 StyleCop 官網下載擴充套件 (http://stylecop.codeplex.com/)[http://stylecop.codeplex.com/]，執行 msi 檔案就可以安裝到 Visual Studio 裏頭了。

### 自訂調整規則集 (rules)
165 條規則其實太多了，很多也是過於太細節的規範 (鳥毛)，基本上公司要視情況自行去定義需要遵守的撰寫規範。

### 編輯 Setting.StyleCop 規則  
![SettingsForStyleCop](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_SettingsForStyleCop.png)

### 針對 class 忽略 StyeCop 規則
在 Error List 中的 Style Cop 錯誤點［右鍵］Show Error Help  
![ShowErrorHelp](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_ShowErrorHelp.png)  
![HowToSuppressViolations](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_HowToSuppressViolations.png)  
![UsingCodeAnalysis](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_UsingCodeAnalysis.png)  
![TooMuchStyleCopRule](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_TooMuchStyleCopRule.png)  

### 整個專案要忽略某個 Style Cop 規則的方法

1. 找到要忽略的規則編號
2. 開啟 StyleCop 儲存的實體檔案，便雙擊開啟
3. 搜尋規則編號(ex. SA1200)
4. 找到規則後將套用規則勾選掉
5. Apply & OK

![SetIgnoreStyleCopRule](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160420_SetIgnoreStyleCopRule.png)


[1]: http://miniasp.kktix.cc/events/stylecop-in-action-online