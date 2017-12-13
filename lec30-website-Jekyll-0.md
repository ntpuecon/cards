---
layout: default-post
---
# 如何在Windows系統下安裝Jekyll?
jkyll是用Ruby語言所寫的工具，所以在安裝jekyll之前我們必須先下載Ruby
### Step 1 Download Ruby
1. 請下載[Ruby2.4](https://rubyinstaller.org/downloads/)的版本，下載後直接執行安裝檔
2. 安裝過程中遇上此步驟請勾選 **Add Ruby executable to your PATH**以及**Associate .rb and .rbw files with this Ruby Installation**  

![RUBYINSTALL]({{site.url}}/minicourses/images/JEKYLL-INSTALL-001.PNG)  

3.安裝完成後，在安裝精靈的最後一步驟可接續安裝MSYS2![install msys2-1]({{site.url}}/minicourses/images/JEKYLL-INSTALL-002.PNG)  
MSYS2是ruby的development kit(可以想像成工具包)，因為在ruby裡面有許多的gem(ruby的套件稱為gem)並不是用ruby語言寫的，所以若要安裝如C語言所寫的gem就必須要靠development kit，也就是MSYS2。
### Step 2 Install MSYS2
直接依照指示完成MSYS2
1. 選擇1(輸入1)先安裝MSYS2 base installation
![install msys2-2]({{site.url}}/minicourses/images/JEKYLL-INSTALL-003.PNG)  
完成後會出現MSYS2的安裝精靈，依照指示點擊**Next**即可完成安裝
![install msys2-3]({{site.url}}/minicourses/images/JEKYLL-INSTALL-004.PNG)
2. 接著對MSYS2進行系統更新，選擇2(輸入2)
![install msys2-4]({{site.url}}/minicourses/images/JEKYLL-INSTALL-005.PNG)
3. 最後選擇3(輸入3)，安裝MSYS2及MINGW的development toolchain
![install msys2-5]({{site.url}}/minicourses/images/JEKYLL-INSTALL-006.PNG)
以上三步即完成MSYS2的安裝

### Step 3 安裝Jekyll
在windows system 安裝jekyll前，必須先調整Ruby gem的來源。   
1. 首先以系統管理員的身分執行**命令提示字元**，並且移除預設的ruby gem source，在命令提示字元中下指令:
```
gem sources -r https://rubygems.org
```

2. 添增新的ruby gem source，在命令提示字元中下指令:
```
gem sources -a http://rubygems.org
```
接著選擇yes(輸入y)，如下圖:
![install jekyll-1]({{site.url}}/minicourses/images/JEKYLL-INSTALL-007.PNG)
3. 安裝Jekyll及Bundler   
jekyll與bundler都是Ruby中的gem，其中jekyll正是我們要用來架設網站的部落格產生器，在架站的過程中我們可以用其他作者製作的網站模板(稱為Jekyll Theme)進行套用，但是這些模板同時可能會用到ruby中其他的gem，bundler的用途就是為了控制這些gem的版本。  
在**命令提示字元**下指令安裝jekyll、bundler這兩個gem。  

```
gem install jekyll bundler
```
以上3步驟完成jekyll的安裝

## 讓jekyll在電腦中運行
首先開啟**命令提示字元**，輸入以下指令，**在c:\建立jekyll資料夾**

```
mkdir c:\jekyll
```
接著進入**jekyll資料夾**，輸入以下指令:

```
cd c:\jekyll
```
在**jekyll資料夾**內建立一個部落格，輸入以下指令(執行指令的路徑必須在jekyll資料夾中):

```
jekyll new my-blog
```
進入 **my-blog** 資料夾，輸入以下指令(執行指令的路徑必須在jekyll資料夾中):

```
cd my-blog
```
最後在my-blog資料夾中運行jekyll，輸入以下指令(執行指令的路徑必須在my-blog資料夾):

```
jekyll serve
```
成功後會出現以下畫面:
![jekyll serve-1]({{site.url}}/minicourses/images/JEKYLL-INSTALL-008.PNG)  

最後在瀏覽器中輸入網址:   http:/127.0.0.1:4000/  
出現以下畫面表示成功!
![jekyll serve-2]({{site.url}}/minicourses/images/JEKYLL-INSTALL-009.PNG)
