# Minicourse-Jekyll建站[0基礎]

# 課程架構
- 了解網站基本架構
- 介紹jekyll
- Jekyll實作(GitHub fork a theme to local)
- Config,Frontmatter說明
- Liquity Language
- 網站實用外掛(Facebook內嵌、埋入Google analytic Tracking Code)
- 在Git Page以自己的網域為域名

## I 了解網站的基本架構
建立一個網站，首先需要具備 網域 主機  網站資料。  
- 網域:每台連上網的電腦都有屬於自己的IP，但IP由數字組成，不方便記憶，於是網域名稱系統(Domain Name System)就誕生了,你可以把IP想像成你的電話號碼，網域名稱(ex.http://emajortaiwan.org)就是你的名子，手機就是Domain Name server，Domain Name System就是電話簿。
- 網站資料:由不同的html檔、css檔組成(簡單的靜態網頁)，html語法是用來呈現網頁的內容，Css語法則是針對html所寫的內容作更進一步的編排、調整(ex.顏色、字體、呈現位置)
- 主機:用來放網站資料

#### 這三樣東西如何連結?
首先我們會把網站資料放進主機，再將主機與網域作連結。我們必須告訴主機我們的域名(主機對網址)，同時也要把主機的ip告訴域名商(網址對主機)，當雙向連結完成，我們只要在瀏覽器中搜尋自己的域名就能夠看見網頁了。


## II 介紹Jekyll

Jekyll 是用Ruby語言所寫的程式，是一個部落格(或靜態網頁)產生器。  
:fa-file:如何安裝Jekyll:[Windows版](https://github.com/tpemartin/E.Major-IT/blob/lec30-website-Jekyll-0/Course-development/lec30-website-Jekyll-0.md),[Mac版](https://jekyllrb.com/docs/installation/)

<br>
優點:

- 所用到的網頁語言單純，不用資料庫，因此利於修改。
- 簡易的liquid language方便撰寫
- 直接以markdown+html寫文章。
- 直接在本機中測試、修改

缺點:
- 因為省去了php(資料庫語法)，所以功能上購物車、會員機制、留言板、討論區、投票區、訊息發佈、商品發佈…等沒辦法使用。(但是可以利用外部嵌入的方式解決多數問題)

## III　Jekyll網站的基本架構
```
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid YAML Frontmatter
```

## StepIV 介紹Config.yaml,Frontmatter
:fa-exclamation-circle:**請注意 在寫yml格式的檔案時不能用 `tab鍵` 來縮排  !!**  
<br>
Config.yml是Jekyll中很特別的檔案，可以讓網站開發者自行定義變數。Config.yml主要是用來定義全域變數。例如:

```
---
title:
google analytics tracking code:
paginator:
ad:
 ad1:
 ad2:
```

而Frontmatter也是yaml格式，但是只需要在html檔案的頁首進行宣告，宣告方式如下，比如說，我們會在寫文章時存成md檔，為了要讓jekyll讀懂這篇文章的layout是甚麼，以及liquid language所引入的變數是甚麼，我們會在文章的最開始寫上FRONTMATTER，同時在上下以`---`包住，告訴JEKYLL這是一個YAML格式:(以下舉例，變數可以依頁面的需求自行定義):

```
---
layout:
date:
catagories:
tag:
---
```
### 常用的yaml variables
jekyll本身已經預設variables,以下將介紹常用變數的用途:
global variables:
```
site:網站
page:頁面
layout:自行設定的版型
content:頁面內容(front matter宣告後，該頁面的內容)
paginator:分頁工具
```

site variables:
```
site.posts:網站中所有posts的清單
site.pages:網站中所有pages的清單
```
page variables:
```
page.categories:該頁面所屬的categoriies
page.date:該頁面的日期
```
其他變數可以到[JEKYLL的官網](https://jekyllrb.com/docs/frontmatter/)查詢。

### V 如何使用Yaml變數?-  使用Shopify的 Liquid Language
Liquid Langeage 是Shopify以ruby所寫的語言，簡單易懂，只要用條件句if,for,else,搭配Liquid Langeage的filter就可以寫出迴圈。以下我們會先介紹基本的語法，再透過實例介紹幾個常用於網站中的迴圈:
##### 基本用法
**I** **引入變數**  
用兩層大括號`{{"變數名稱"}}`，將先前在Config.yml或Front matter定義好的變數引入網頁中。  

**II** **迴圈**  
以`for`定義範圍,再以`if`設定條件，最後以`{%endif%}` `{%endfor%}`關閉迴圈

```
{% for...in... %}
{% if...%}
...
...
...
{% endif %}
{% endfor %}
```

##### 實例介紹
**I** 列出所有category屬於"A"的文章"標題"  
先假設某篇文章的Front matter為:

```
---
layout: post
title: my-first-post
category: A
published: true
permalink: my-first-post
---

```
寫一個迴圈
```
{% for post in site.posts %}
{% if post.category contains "A" %}

<a href="{{ post.url }}">{{ post.title }}</a>

{% endif %}
{% endfor %}

```
output:

```
my-first-post
```

**II** 藉由引入include 資料夾的檔案，寫出一個頁面layout，首先必須先了解一個網站頁面的結構:

```
<!DOCTYPE html>
<html>
<head>
...
...
..
</head>

<body>

<header>
...
...
...
</header>

<footer>
...
...
...
</footer>

</body>

</html>
```

可以看見網站主要由 `<head>` `<body>` `<header>` `<footer>` 所組成，Jekyll的好處是讓網站開發者可以將這些網頁組成要數分別以不同的html檔存在`include`資料夾中，再用Liquid Language引入同一個html檔案中。  
以下用一個Layout舉例:  
假設 `head.html` `header.html` `footer.html` 已經寫成html檔存在`include`資料夾中
```
<!DOCTYPE html>
<html>
{% include head.html %}
<body>
{% include header.html %}
{{ content }}
<footer>
 {% include footer.html %}
</footer>
</body>
</html>

```
我們把以上code存成html檔，命名為`default.html`，當我們要寫新的post或page時，我們便可以直接在Front Matter 宣告 `layout: default`,接著只需寫該頁面的`特定內容`(`{{ content }}`) :  

```
---
layout: default
---
內容可以用html或markdown撰寫
...
...
...

```
### VI 網站行銷常用的工具
#### 嵌入FB social plugin  
Step1 開通FB Developer 帳號  
Step2 創造一個APP  
Step3 將 `Java Script SDK code` 貼在`<body>`後
Step4 將`外掛嵌入碼`貼在想要呈現的位置(例如`side bar`,`footer`)  
**[Youtube教學](https://www.youtube.com/watch?annotation_id=annotation_243482009&feature=iv&src_vid=WNHfVdK8xik&v=5o7sKq881rw)**

#### 嵌入Google analytics tracking code
Step1 新建帳戶  
Step2 在新建帳戶下新建資源  
Step3 取得追蹤碼並置於`<head>...</head>`中
Step4 連線至網站中，並在Google analytics看是否有採集到數據(通常隔天才能確定有沒有成功)  

### VII 在Git Page以自己的網域為域名
Step1 在github中新增名為`CNAME`的檔案(不需附檔名)  
Step2 在`CNAME`檔案中寫下自己租用的網域
Step3 到網域服務商填入Gitpage的`A 紀錄` =192.30.252.153 以及 192.30.252.154 (共兩個A紀錄)  
詳細[教學資源](https://hackernoon.com/how-to-set-up-godaddy-domain-with-github-pages-a9300366c7b)

---
