# Exepro 又干啥了？
作者 [8bd8.github.io
（后面以 黑客000 代替）](https://bbs.deepin.org/user/291275) 于 2022 年 12 月 2 日于 Deepin 论坛发布帖子：《exePro-13 正式版发布！》  
不过因为论坛帖子被删除，但可见：https://github.com/8bd8/exepro-app ，这里还有 
![image.png](https://storage.deepin.org/thread/202212031022131166_image.png)   
排除掉 UI 和功能相似外，发现于 main 含义以下代码：  
```python
deletexMenu=AdvancedOptions.addAction('删除无用软件')
def deletex():
    if QMessageBox.question(window, "是否删除", "是否删除wine熨刑器以及uengine熨刑器",QMessageBox.Yes,QMessageBox.No)==QMessageBox.Yes:os.system("pkexec apt -f autopurge *wine-runner -y&&pkexec apt -f autopurge *uengine-runner -y")
deletexMenu.triggered.connect(deletex)
```
此代码可以移除包名为 `spark-uengine-runner` 和 `spark-deepin-wine-runner` 的 UEngine 运行器（旧版本）和 Wine 运行器，调用方法如下：  
![image.png](https://storage.deepin.org/thread/202212031019557743_image.png)  
调用效果：  
![image.png](https://storage.deepin.org/thread/202212031020321968_image.png)  
我们引用 Deepin 论坛版主大大的一句话：  
> 建议所有人 抵制 exePro ，为了自身利益，其采取的手段包括但不限于攻击 @gfdgd xi 的服务器，辱骂统信 UOS 用户，提供卸载 Wine 运行器 的功能，其行为已构成不正当竞争，并威胁到统信软件的名誉权。

## 为何有攻击 @gfdgd xi 的服务器？
他自己都说了：  
![QQ图片20221203105057.jpg](https://storage.deepin.org/thread/20221203105113783_QQ图片20221203105057.jpg)  
此为异常请求日志节选（攻击接口已屏蔽，为了防止被2次攻击，日志不会显示被攻击接口）：  
因为是走内网穿透，所以无法显示正确的 IP 地址：  
（不过他还没刷完的时候我就停服务器了）  
> 谁家下载量的请求是这样频繁的
```log
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:23 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:23 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:24 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:24 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:24 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:25 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:25 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:26 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:26 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:26 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:27 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:27 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:27 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:28 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 203 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:93.0) Gecko/20100101 Firefox/93.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:28 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:28 +0800] "GET /favicon.ico HTTP/1.1" 200 5859 "https://xxx?Version=2.5.0" "Mozilla/5.0 (X11; Linux x86_64; rv:93.0) Gecko/20100101 Firefox/93.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:28 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:29 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:29 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:29 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:30 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:30 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:30 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:31 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:31 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:31 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:32 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:32 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:33 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:33 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:33 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:34 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:34 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:34 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:35 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:35 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:36 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:36 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:36 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:37 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:37 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:37 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:38 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:38 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:38 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:39 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:39 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:40 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:40 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:40 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:40 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:41 +0800] "GET /uengine-runner/Install.php?Version=1.8.2 HTTP/1.1" 200 147 "-" "curl/7.64.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:41 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:41 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
127.0.0.1:80 127.0.0.1 - - [01/Dec/2022:11:25:41 +0800] "GET xxx?Version=2.5.0 HTTP/1.1" 200 147 "-" "curl/7.81.0"
```

## 为何有 辱骂统信 UOS 用户？
于未公开发布的 Alpha2 中，含有侮辱统信 UOS 用户的代码，下面是该版本程序 UI：  
![image.png](https://storage.deepin.org/thread/202212031048261359_image.png)  
其中程序含有代码：  
```python
if "UOS" in platform.version() or "Union" in platform.version():
    QMessageBox.critical(window, "滚蛋", "捅信傻逼OS用户请滚蛋",QMessageBox.Ok)
    quit()

```

## Exepro 13Alpha2 下载地址：
可见：https://gfdgdxi.lanzoue.com/icqdx0hmkkej
最新版本的 Exepro 可见：https://setup.lanzoum.com/b03doi60f 密码:exepro  