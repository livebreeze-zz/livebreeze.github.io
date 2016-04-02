---
layout: post
title:  "Jekyll 新手問題"
date:   2016-04-02 20:17:00 +0800
categories: Jekyll
---

最近開始改用 github.io 撰寫部落格，搭配官方建議的開源靜態網頁產生工具 **[jekyll](https://jekyllrb.com/)** (念起來像"結果")，

因為是個工具，一開始難免會遇到一些新手問題，當對於工具一知半解就會開始卡老半天，

雖然官方也有 [Guide](https://jekyllrb.com/docs/home/) 可以參考學習，不過都是英文... 讀起來有些睏，

所以就是一邊使用一邊查資料，從問題中學習 @_@a

### 問題一: 為何我在 _posts 的文章沒有產生出來
檢查　post 開頭的文章時間設定，是否是今天以前，  
假設目前時間是 `2016/04/02 20:12:00`，則 `2016/04/02 20:12:00` 之後的文章就不會產生出來 　　
        
    ---
    layout: post
    title:  "Jekyll 新手問題"
    date:   2016-04-02 22:08:00
    categories: Jekyll
    ---
    
上面這樣的設定文章就不會被 jekyll 產生出來，原因是 jekyll 有個 future-posts 的功能可以設定，  
如果不想要這樣的設定，在 `_config.yml` 裡面增加 `future:true` 設定，  
需要注意的是，這個判斷時間有時區影響，如果在台灣，要在 post 的 date 設定加上 `+0800`

官方說明:  
All my posts are gone! Where’d they go!Permalink  
[http://jekyllrb.com/docs/upgrading/2-to-3/#future-posts](http://jekyllrb.com/docs/upgrading/2-to-3/#future-posts)