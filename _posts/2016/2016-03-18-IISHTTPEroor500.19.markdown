---
layout: post
title:  "IIS 無法啟用 - HTTP Error 500.19"
date:   2016-03-18 10:28:00
categories: Server
---

今天在新的 window 10 想要架設 IIS 站點，依照慣例，開啟 windows 功能("Turn windows features on or off" )，然後將 IIS 開啟~
開啟的功能便依循預設的方式開啟。結果 IIS 10 可以正常啟動與顯示出歡迎頁面，結果當我把專案 publish 到 wwwroot 後，悲劇出現了!! 

![20160402IISHTTPError500.19.png](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160402IISHTTPError500.19.png)

直覺又是 MAC 裝 windows，有可能又是 folder 權限問題，所以想盡辦法去開啟 secure.... but 無效，搞了老半天，終於找到啦!

- HTTP Error 500.19 and error code : 0x80070021  
[http://stackoverflow.com/questions/20048486/http-error-500-19-and-error-code-0x80070021](http://stackoverflow.com/questions/20048486/http-error-500-19-and-error-code-0x80070021)
- IIS - this configuration section cannot be used at this path (configuration locking?)  
[http://stackoverflow.com/questions/9794985/iis-this-configuration-section-cannot-be-used-at-this-path-configuration-lock/12867753#12867753](http://stackoverflow.com/questions/9794985/iis-this-configuration-section-cannot-be-used-at-this-path-configuration-lock/12867753#12867753)

> I had the same problem. Don't remember where I found it on the web, but here is what I did:
>
>	* Click "Start button"
>	* in the search box, enter "Turn windows features on or off"
>	* in the features window, Click: "Internet Information Services"
>	* Click: "World Wide Web Services"
>	* Click: "Application Development Features"
>	* Check (enable) the features. I checked all but CGI.


 簡單的來說，就是 **在 windows features 裡的 IIS 功能沒有開完全!!** ...
 
 ![20160402_OpenIISFeatures](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/20160402_OpenIISFeatures.png)
 
 如果依照預設只勾選到最外層的 IIS 啟用設定，並不會將 **Application Development Features** 啟用，所以必須動動手把她開啟咧。
 
 THE END...
 
 ---
 
> 2016/03/28 update 

後續又碰到 IIS 對 localDb  無法連線的問題，基本上確實是權限的問題，

暫時先不研究這部分權限問題，為了避免後續麻煩，所以將資料改連向 SQL Express 就可以了。



