---
layout: post
title:  "讓 Chrome Dev Tool 也能 dark theme (DevTools Theme: Zero Dark Matrix)"
date:   2016-04-22 00:05 +0800
categories: Tools
---

# Update

> 2017/02/02 更新

最近發現 Chrome 已經有內建黑暗版的開發介面了，設定也非常的簡單(就在第一個設定 XD)，不過還是截了兩張圖來見證一下

- Chrome 內建的顯示樣式  
![ChromeDevToolDarkTheme](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2017/20170202_ChromeDevToolDarkTheme.jpg)

- 設定  
![ChromeDevToolDarkThemeSettings](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2017/20170202_ChromeDevToolDarkThemeSettings.jpg)

# 前言

身為網頁開發人員，長時間盯著開發工具鐵定是避免不了，而螢幕預設的白底總是讓人容易眼睛酸澀，

從 Visual Studio 2012 開始便內建深色主題 (dark color theme) 的開發環境，套用後舒服多拉！

![VS2012SartPage](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160421-VS2012SartPage.png)


而強大又好用的前端開發工具 **Chrome Developer Tools** 該如何方便的套用深色樣式呢? 

使用 chrome 擴充套件 **[DevTools Theme: Zero Dark Matrix](https://chrome.google.com/webstore/detail/devtools-theme-zero-dark/bomhdjeadceaggdgfoefmpeafkjhegbo?hl=zh-TW)**

# 安裝方法:

1. 安裝 chrome 擴充套件  DevTools Theme: Zero Dark Matrix  
![DevToolsThemeZeroDarkMatrix](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160421-DevToolsThemeZeroDarkMatrix.png)

2. 開啟 chrome 開發人員設定連結 -> `chrome://flags/#enable-devtools-experiments`，將「開發人員工具實驗性功能」啟用  
![ChromeDeveoperExperimentsSetting](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160421-ChromeDeveoperExperimentsSetting.png)

3. 在 Developer Tools Setting 裡面就會有 Experiments 選項，核選 「Allow custom UI themes」設定  
![AllowCustomUIThemes](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160421-AllowCustomUIThemes.png)

4. 關閉 Chrome Developer Tool 再重開就完成拉！( 撒花～  
![ChromeDeveloperToolBlackTheme](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160421-ChromeDeveloperToolBlackTheme.png)


