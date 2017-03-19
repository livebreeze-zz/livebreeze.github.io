---
layout: post
title:  "Jekyll 新手問題"
date:   2016-04-02 20:17:00 +0800
categories: Jekyll
tag: [Jekyll, Githubio]
---

最近開始改用 github.io 撰寫部落格，搭配官方建議的開源靜態網頁產生工具 **[jekyll](https://jekyllrb.com/)** (念起來像"結果")，  
因為是個工具，一開始難免會遇到一些新手問題，當對於工具一知半解就會開始卡老半天，  
雖然官方也有 [Guide](https://jekyllrb.com/docs/home/) 可以參考學習，不過都是英文... 讀起來有些睏，  
所以就是一邊使用一邊查資料，從問題中學習 @_@a

> 2017/03/19 Update   
> 下面有熱心的 Rhadow's 分享中文的說明，大致上剛開始設定 Github.io 與 Jekyll 是很好的參考文章喔   
> [Jekyll x Github x Blog (Part 1)](https://rhadow.github.io/2015/02/18/Jekyll-x-Github-x-Blog-Part1/)  

### 問題一：為何我在 _posts 的文章沒有產生出來
檢查　post 開頭的文章時間設定是否偷跑到未來了，  
假設目前時間是 `2016/04/02 20:12:00`，則 `2016/04/02 20:12:00` 之後的文章就不會產生出來 　　
        
    ---
    layout: post
    title:  "Jekyll 新手問題"
    date:   2016-04-02 22:08:00
    categories: Jekyll
    ---
    
上面這樣的文章設定就不會被 jekyll 產生出來，原因是 jekyll 有個 future-posts 的功能可以設定，  
如果不想要這樣的設定，在 `_config.yml` 裡面增加 `future:true` 設定，  

需要注意的是，這個 future-posts 的功能，判斷的時間是標準時區，  
所以在台灣，需要在 post 的 date 設定加上 `+0800` 判斷才會正確。

     date: 2016-04-02 22:08:00 +0800

官方說明：  
All my posts are gone! Where’d they go!Permalink  
[http://jekyllrb.com/docs/upgrading/2-to-3/#future-posts](http://jekyllrb.com/docs/upgrading/2-to-3/#future-posts)


### 問題二： 如何使用 jekyll 載入 js 檔案

- 所有頁面共用的 js
    1. 在 `_includes` 資料夾中加入自訂的資料夾 `scripts` (方便管理)
    2. 在自訂的 `_includes/scirpts` 資料夾加上新的 js 檔案
    3. 在 `_layout/default.html` 內容加上 scripts tag，並在區塊內載入上面加好的檔案  

```
// _layouts/default.html
<script>
    {% include scripts/base.v0.js %}
</script>
``` 

- 不同「文章」載入不同的 js 方式  
    1. 與上1同
    2. 與上2同
    3. 在 _layouts/post.html 最下方載入 post 設定的 post  
    4. 在需要額外載入 js 的 _posts/文章 設定加上 js 來源 

```
// step 3
// _layouts/post.html
<script>
    { % for js in page.jsarr % }
        <script>
            { % include {{js}} % }
        </script>
    { % endfor % }
</script>

// 注意, `{`與`%` 中間沒有空白
```

```
// step 4
    ---
    layout: post
    jsarr: [scripts/test.js]
    ---
```

參考資料: [Using Custom Javascript In Jekyll Blogs](http://etosch.github.io/2016/03/09/using-custom-javascript-in-jekyll-blogs.html)