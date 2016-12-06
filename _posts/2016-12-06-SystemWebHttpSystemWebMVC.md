---
layout: post
title:  "[TechNote] System.Web.Http 和 System.Web.Mvc"
date:   2016-12-06 21:05 +0800
categories: TechNote
author: Sean.C
tag: [technote, C#, MVC]
bgimgurl: https://raw.githubusercontent.com/livebreeze/BlogImages/e5ae2b0d2d34430043ac20879b52243eb0067a9e/Images2016/20160803_PostBGImg.jpg
---

# 前言
在 support mobile service api 的時候，碰到 Get 沒辦法調用成功的問題，api 會返回 "405 mehotd not allowed web api" 的 error 訊息。

# 解決方法
簡單查了一下估狗大神，好像是 Get 的命名問題，在 method 前面加個 Get 前墜就可以解決了。  
在 stack overflow 找到的問答:  
[405 method not allowed web api](https://blogs.msdn.microsoft.com/benjaminperkins/2015/07/01/asp-net-webapi-results-in-a-405-method-not-allowed-http-response/)  


不過確切的問題原因不知道，於是乎需要深入來追查一下，發現是使用的 framework 問題，改用 using System.Web.Http 就沒有這樣的問題了。  
原因在於 System.Web.Http 是用於 Web Api 而 System.Web.Mvc 是為提供 mvc 的框架。  
[System.Web.Mvc.ActionFilterAttribute vs System.Web.Http.Filters.ActionFilterAttribute](http://stackoverflow.com/questions/12606202/system-web-mvc-actionfilterattribute-vs-system-web-http-filters-actionfilterattr)

