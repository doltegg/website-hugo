---
title: "在 Jupyter Notebook 上安裝 R (Windows 10)"
date: 2018-07-12T21:55:00+08:00
draft: false
tags: ["R", "Data Science"]
share: true
---

![IRkernel-1](/images/r-kernel-for-jupyter-notebook/IRkernel-1.png)

最近為了某個目的，想在 Jupyter Notebook 上寫 R code。利用 IRkernel 就能達到這件事，然而在安裝的過程中發生了一些問題，因此做了很多搜尋，將操作步驟整理在此，希望能幫助到一些人，同時也紀錄自己對於電腦世界的懵懂無知。

---

### 安裝 IRkernel 的前提 (Requirements)

1. 安裝好 R （我的版本是 3.4.1，若還有安裝 RStudio 更好）。
2. 安裝好 Jupyter Notebook （我是用 Anaconda 安裝的）。 

### 此路不通 (Not Work for Me)

一開始我按照[這個網站](http://white5168.blogspot.com/2017/09/anaconda-rpythonr.html#.W0dfsWb3X-b)的步驟操作，在 Anaconda Prompt 內打入：

```
conda update anaconda
conda install -c r r-essentials
```

在筆電和桌電上試驗都在第二步出現了 Error，沒辦法安裝，查了 google 和 stackoverflow 都找不到解答。（不過好多東西我都看不懂，所以也有可能是有解的。）之後還在 YouTube 看別人怎麼安裝，但對我來說還是不成功。

### 解法 (My Solution)

後來在某影片中的某片段看到一個似乎是 [IRkernel 的官方網址](https://irkernel.github.io)，按照裡面的方法後，就安裝成功了！（心得：看官方文件還是最準的 OTZ）

#### Step 1

在 RStudio 的 Console 內打入：

```
install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest')) 
devtools::install_github('IRkernel/IRkernel')
```

#### Step 2 (Wrong)

在 RStudio 中的 Console 內打入：

```
IRkernel::installspec()
```

結果出現 Error：

![IRkernel-2](/images/r-kernel-for-jupyter-notebook/IRkernel-2.png)

後來在 [Stackoverflow](https://stackoverflow.com/questions/44056164/jupyter-client-has-to-be-installed-but-jupyter-kernelspec-version-exited-wit/44108916) 這篇上找到解法 (第二個回答)

#### Step 2 (Correct)

打開 Anaconda Prompt (或是用 Windows 內建的 cmd 好像也可以)，更改路徑到裝有 R.exe 的資料夾 (以下是我的路徑)：

```
cd "C:\Program Files\R\R-3.4.1\bin"
```

![IRkernel-3](/images/r-kernel-for-jupyter-notebook/IRkernel-3.png)

接著打入這行，進入 R。

```
R.exe
```

重新打入剛剛在 RStudio 中失敗的這行：

```
IRkernel::installspec()
```

沒有出現錯誤！！！先關掉 R，不用儲存空間圖案：

```
q()
```

#### Step 3

先回到你想要的路徑，再打開 Jupyter Notebook：

```
cd "你的某資料夾"
jupyter notebook
```

出現 R 的選項了！！！

![IRkernel-4](/images/r-kernel-for-jupyter-notebook/IRkernel-4.png)

畫個圖試試看：

![IRkernel-5](/images/r-kernel-for-jupyter-notebook/IRkernel-5.png)

好感動啊！！！！！以上就是安裝 IRkernel 的方法，感謝大家看到這裡。