---
title: "Python 中 sys.argv[] 配合 Shell Script 的使用方法"
date: 2018-07-12T22:25:02+08:00
draft: false
tags: ["Python"]
share: true
---

最近在寫李宏毅老師的 [ML 課程作業](https://ntumlta.github.io/2017fall-ml-hw2/)時，第一次接觸了shell script，也終於弄懂 sys.argv[] 的用法。過程中看了網路上許多參考資料的介紹，總覺得對於我這個新手來說太過複雜，故在此稍作整理並紀錄。

### 第一步：建立含有 sys.argv[] 的 .py 文件

![shell-1](/images/sysargv-shell/shell-1.png)

使用任意文字編輯器建立 .py 文件，如圖中的 test_code.py。

### 第二步：建立 .sh 文件

![shell-2](/images/sysargv-shell/shell-2.png)

在 terminal 或 cmd 輸入以下指令：

```
touch shell_name
```

touch 指令可以建立新的 .sh 文件，後面接你要的文件名稱，如圖中的 test_shell（注意這邊不用打副檔名 .sh）。

好的，到目前為止，資料夾中已有兩個檔案：test_code.py 和 test_shell.sh

![shell-3](/images/sysargv-shell/shell-3.png)

接下來我們要在 test_shell.sh 中打一些東西：

![shell-4](/images/sysargv-shell/shell-4.png)

```
#!/bin/bash
python3 your_code.py $1...
```

1. \#!/bin/bash 這行告訴系統以 bash（一種 shell）執行這個 .sh 檔。
2. python3 後面接要執行的 .py 文件，再後面接 $1、$2 … ，看你 .py 中 sys.argv[] 數字到多少就打到多少，因為 $1 之後會對應 sys.argv[1]、$2 會對應 sys.argv[2] … 以此類推。

### 第三步：傳遞參數 (passing arguments)

![shell-5](/images/sysargv-shell/shell-5.png)

在 terminal 或 cmd 輸入以下指令：

```
sh ./shell_name arg1 arg2
```

sh 後面接 .sh 文件的路徑，再後面接你要傳遞給 sys.argv[1] 和 sys.argv[2] 的參數。**也就是說，terminal 中的 arg1 傳遞參數給 .sh 文件中的 $1，$1 再傳遞給 .py 文件中的 sys.argv[1]。**

那你可能會想，那 sys.argv[0] 呢？答案就在上面的輸出結果中。

沒錯，sys.argv[0] 就是 test_shell.sh 中執行的 **.py 文件名稱** (test_code.py)

#### References

1. [Python中 sys.argv[]的用法简明解释](https://www.cnblogs.com/aland-1415/p/6613449.html)
2. [李宏毅老師 ML 課程 HW2 TA Hour Slide](https://docs.google.com/presentation/d/1nOJkDRXDdORwkwibzX55w7jGOyB-rPjCOeRpwaZ82as/edit#slide=id.g1d460c2d77_0_60)