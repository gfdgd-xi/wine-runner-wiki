你可能会需要运行其他的 wine，因为 deepin-wine 还是有很多不完美，例如说不够新（截止更新 deepin-wine 团队已经发表 deepin-wine5,而 wine 团队发布了 wine 6）、不支持 64 位程序、其他发行版安装困难等会需要使用到其他的 wine
这个程序可以使用其他的 wine，虽然已经写死了只能用 deepin-wine 和 deepin-wine5，但因为这是用 Python3 编写，运行的只是文本文档，因此可以修改，修改方法如下：

1、使用自己熟悉的编辑器打开源码（主程序），需要有读写的权限（如是 git 获取，源码在 git 获取到的文件夹的 main.py 文件；如是安装了 deb 包，源码在 /usr/bin/deepin-wine-runner 文件）
![输入图片说明](https://images.gitee.com/uploads/images/2021/0213/143240_50f577bb_7896131.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2021/0213/143324_456674d4_7896131.png "屏幕截图.png")

2、找到以下代码（视实际情况而定）

```
o1 = tk.OptionMenu(window, o1_text, "deepin-wine", "deepin-wine5") # 创建选择框控件
```
在 "deepin-wine5" 后面添加要使用的 wine 的程序名，如下（以添加 wine64 为例）：

```
o1 = tk.OptionMenu(window, o1_text, "deepin-wine", "deepin-wine5", "wine64") # 创建选择框控件
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0213/143753_ad53bfda_7896131.png "屏幕截图.png")
然后保存

3、运行查看效果
![输入图片说明](https://images.gitee.com/uploads/images/2021/0213/143906_0fd2cfc8_7896131.png "屏幕截图.png")
