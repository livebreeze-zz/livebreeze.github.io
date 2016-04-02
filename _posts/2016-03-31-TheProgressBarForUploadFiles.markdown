---
layout: post
title:  "建立檔案上傳 progress 進度條"
date:   2016-03-31 21:00:00
categories: LearningNote
---

## Backgroud
最近在寫內部系統的工具，其中一個功能是需要將一些文件(像是 email 或者文件等等)，
能夠利用拖拉或者選擇檔案的方式，來將檔案上傳到 server 端儲存，
藉此機會練習一下，如何使用 angular or jQuery 將檔案透過 HTML 的 FileReader 上傳到 server 端，並且能夠顯示進度條，
主要 follow 黑大的文章一步步來，但因為是使用 angular ，而不是依照範例中的 Knockout.js，所以實現的過程中也遇到一些問題。

以下是主要的參考資料:

- [HTML5檔案上傳進度條 by 黑大](http://blog.darkthread.net/post-2014-03-09-upload-progress-bar-w-xhr2.aspx)
- [AJAX 利用 XHR2 Progress Event 實作下載進度列](http://blog.toright.com/posts/3585/ajax-%E5%88%A9%E7%94%A8-xhr2-%E5%AF%A6%E4%BD%9C%E4%B8%8B%E8%BC%89%E9%80%B2%E5%BA%A6%E5%88%97-progress-event.html)
- [AngularJs: How to check for changes in file input fields?](http://stackoverflow.com/questions/17922557/angularjs-how-to-check-for-changes-in-file-input-fields )


主要實作上傳的 jQuery ajax 內容

 {% highlight javascript %}
 // 以 XHR 上傳原始格式
            $.ajax({
                type: "POST",
                url: "/ajax/upload?fileName=" + file.name,
                contentType: "application/octect-stream",
                processData: false, // 不做任何處理，只上傳原始資料
                data: data,
                xhr: function () {
                    // 建立 XHR 時，加掛 onprogress 事件
                    var xhr = $.ajaxSettings.xhr();
                    xhr.upload.onprogress = function (event) {
                        //file.uploadedBytes(event.loaded);
                        if (event.lengthComputable) {
                            $('#myProgress').attr('max', event.total);
                            $('#myProgress').attr('value', event.loaded);
                        }
                    };

                    return xhr;
                }
            })
 {% endhighlight %}
 
 
### 遇到問題
     
在另外的 web site 也實現照片上傳的功能，結果改到後來突然上傳的檔案都只剩下 1KB  
![upload1kbFileError](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/upload1kbFileError.png)

才發現在 ajax post 的地方，因為亂 copy 別人的 solution，結果要上傳的資料，在送出前經過了 JSON.stringify 處理  
![upload1kbFileErrorCode](https://raw.githubusercontent.com/livebreeze/BlogImages/master/Images2016/upload1kbFileErrorCode.png)

一直懷疑到底是 browser 還是 server 哪邊傳輸有問題，原來是 JSON.stringify 這邊導致上傳資料被截斷成只有 1kb....   END



### 進階練習

搭配使用 SingalR 上傳進度條  
- [[C#]使用SignalR 實作檔案上傳進度條 by 黑大](https://dotblogs.com.tw/ricochen/2014/10/16/146962)


