<p width=100px align="center"><img src="https://storage.deepin.org/thread/202208031419283599_deepin-wine-runner.png"></p>
<h1 align="center">Wine 运行器</h1>
<hr>

## 介绍
一个图形化了以下命令的程序  
```bash
env WINEPREFIX=容器路径 wine（wine的路径） 可执行文件路径
```
让你可以简易方便的使用 wine  
是使用 Python3 的 PyQt5 构建的    
（自己美术功底太差，图标只能在网络上找了）    
（测试平台：deepin 20.7；UOS 家庭版 21.3.1；Ubuntu 22.04；Ubuntu 20.04；UOS 专业版 1050）    
![截图_选择区域_20221002221112.png](https://storage.deepin.org/thread/202210022215217037_截图_选择区域_20221002221112.png)  
而打包器可以方便的把您的 wine 容器打包成 deb 包供他人使用，程序创建的 deb 构建临时文件夹目录树如下：  
```bash
/XXX
├── DEBIAN
│   └── control
│   └── postrm（可选）
└── opt
└── apps
    └── XXX
        ├── entries
        │   ├── applications
        │   │   └── XXX.desktop
        │   └── icons
        │       └── hicolor
        │           └── scalable
        │               └── apps
        │                   └── XXX.png（XXX.svg）
        ├── files
        │   ├── files.7z
        │   └── run.sh
        └── info

11 directories, 6 files
```

## 软件架构
i386、amd64 和 arm64，deepin-wine、deepin-wine5、wine、wine64、deepin-wine5-stable、deepin-wine6-stable、spark-wine7-devel、ukylin-wine 运行在哪就运行在哪  
理论上支持全架构，如果 Python 能运行的话  
非 X86 架构会利用到 `box86`、`exagear`等技术  

## 分支介绍
### main 分支
主分支，稳定分支
### Alpha 分支
开发版分支，一般不稳定，有许多 bug

## 版本区分
### 无特殊标识
普通版本（一般来自 Gitee、Github、Gitlink 等渠道）  
### 版本号带`-spark`
星火应用商店版本  
### 版本号带`-uos`
深度应用商店版本，一般带免开开发者模式签名  
### 包名带`-52`
吾爱论坛专版，只在吾爱论坛发布，功能会阉割（如更新、评分、bug反馈功能等等），一般建议使用上面的三个版本  
![image.png](https://storage.deepin.org/thread/202209251259142818_image.png)  
（没人喜欢看到这个无法连接服务器吧）    

## 使用说明
### 均在软件的“小提示”里有说明
### 运行器
1、使用终端运行该程序，可以看到 wine 以及程序本身的提示和报错;  
2、wine 32 位和 64 位的容器互不兼容;  
3、所有的 wine 和 winetricks 均需要自行安装（可以从 菜单栏=>程序 里面进行安装）  
4、本程序支持带参数运行 wine 程序（之前版本也可以），只需要按以下格式即可：  
```bash
exe路径\' 参数 \'
```
即可（单引号需要输入）  
5、wine 容器如果没有指定，则会默认为 ~/.wine  
6、如果可执行文件比较大的话，会出现点击“获取该程序运行情况”出现假死的情况，因为正在后台读取 SHA1，只需要等一下即可（读取速度依照您电脑处理速度、读写速度、可执行文件大小等有关）  
7、对于非 X86 的用户来说，请不要使用本程序自带的 Wine 安装程序和 Windows 虚拟机安装功能（检测到为非 X86 架构会自动禁用）  
8、如果非 X86 的用户的 UOS 专业版用户想要使用的话，只需要在应用商店安装一个 Wine 版本微信即可在本程序选择正确的 Wine 运行程序   
9、在使用 linglong 包的 Wine 应用时，必须安装至少一个 linglong 的使用 Wine 软件包才会出现该选项，而程序识别到的 Wine 是按 linglong 的使用 Wine 软件包名的字母排序第一个的 Wine，且生成的容器不在用户目录下，而是在容器的用户目录下（用户目录/.deepinwine、/tmp、桌面、下载、文档等被映射的目录除外），同理需要运行的 EXE 也必须在被映射的目录内  
10、如果是使用 Deepin 23 的 Wine 安装脚本，请切记——安装过程会临时添加 Deepin 20 的 apt 源，不要中断安装以及千万不要中断后不删除源的情况下 apt upgrade ！！！中断后只需重新打开脚本输入 repair 或者随意安装一个 Wine（会自动执行恢复操作）即可。以及此脚本安装的 Wine 无法保证 100% 能使用，以及副作用是会提示  
```bash 
N: 鉴于仓库 'https://community-packages.deepin.com/beige beige InRelease' 不支持 'i386' 体系结构，跳过配置文件 'main/binary-i386/Packages' 的获取。  
```
![image.png](https://storage.deepin.org/thread/202208131811324016_image.png)  
### 打包器
1、deb 打包软件包名要求：  
软件包名只能含有小写字母(a-z)、数字(0-9)、加号(+)和减号(-)、以及点号(.)，软件包名最短长度两个字符；它必须以字母开头
2、如果要填写路径，有“浏览……”按钮的是要填本计算机对应文件的路径，否则就是填写安装到其他计算机使用的路径  
3、输入 wine 的容器路径时最后面请不要输入“/”  
4、输入可执行文件的运行路径时是以“C:/XXX/XXX.exe”的格式进行输入，默认是以 C： 为开头，不用“\”做命令的分隔，而是用“/”  
5、.desktop 的图标只支持 PNG 格式和 SVG 格式，其他格式无法显示图标  
![image.png](https://storage.deepin.org/thread/202207190820337719_image.png)
### 基于统信 Wine 生态适配脚本的打包器
第一个文本框是应用程序中文名  
第二个文本框是应用程序英文名  
第三个文本框是最终生成的包的描述  
第四个选择框是desktop文件中的分类  
第五个输入框是程序在 Wine 容器的位置，以 c:\\XXX 的形式，盘符必须小写，用反斜杠，如果路径带用户名的话会自动替换为$USER  
而 StartupWMClass 字段将会由程序自动生成，作用如下：  
desktop文件中StartupWMClass字段。用于让桌面组件将窗口类名与desktop文件相对应。这个值为实际运行的主程序EXE的文件名，wine/crossover在程序运行后会将文件名设置为窗口类名  
第六个输入框是最终生成的包的包名,包名的命名规则以deepin开头，加官网域名（需要前后对调位置），如还不能区分再加上应用名  
最后一个是最终生成的包的版本号，版本号命名规则：应用版本号+deepin+数字  
![image.png](https://storage.deepin.org/thread/202207190822204627_image.png)



## 源码安装教程
1. 安装需要的依赖  
```bash
sudo apt install git make
```
2. 下载仓库  
```bash
git clone https://gitee.com/gfdgd-xi/deep-wine-runner.git
cd deep-wine-runner
```
3. 从源码运行程序（如果是从源码安装请跳过这一步）  
```bash
make depend
make run
```
4. 从源码安装程序  
```bash
make install
```

## 对于 Deepin/UOS（AMD64 平台）小白如何使用该程序？
下面是送给小白的 wine 运行器简单使用方法，先声明，wine 并***不能完美的运行所有 exe 文件***，利用此 wine 运行器简易安装可执行文件的方法如下：  

1. 安装本程序
2. 在应用商店里随便安装一个 QQ 或者微信等基于 deepin-wine6-stable 打包的应用
   ![image.png](https://storage.deepin.org/thread/202207061542433333_image.png)
3. 找到需要安装的 exe，双击或者右键=》打开方式=》wine 运行器打开
   ![image.png](https://storage.deepin.org/thread/202207061543443740_image.png)
4. 点击“运行程序”即可
   ![image.png](https://storage.deepin.org/thread/202207191920282406_image.png)


## 稍微讲一下目前 deepin 23 Preview 运行自定义 exe 的方法（Wine 运行器均已支持）

### 方法一

随便安装一个 linglong 格式包的 wine 程序（要记住包名），然后在终端输入

```bash
ll-cli run 包名 --exec '/bin/deepin-wine6-stable'
```

即可，缺陷可看运行器上方小提示第 6 点

### 方法二（容易翻车）

添加 Deepin 20 的**官方源和商店源**，然后输入如下的命令：**切记不能sudo apt upgrade**，会出现的问题可以看运行器的小提示第 7 点，以及无法保证所有 Wine 均可运行

```bash
sudo dpkg --add-architecture i386
sudo apt update
# 安装普通的 Wine
sudo apt install wine
# 安装 deepin-wine5-stable（本机测试 X64 的 Wine 跑不了）
sudo apt install deepin-wine5-stable
# 安装 deepin-wine6-stable
sudo apt install deepin-wine6-stable
```
**使用完后最好删除掉 Deepin 20 的官方源和商店源，防止出问题**  
可以看 [@ThinkYoung](user/18570) 写的 https://bbs.deepin.org/post/241148，可以参考借鉴  

### 方法三
我不知道了，希望能有大佬提供更好的解决方案

## 下载链接
Gitee：https://gitee.com/gfdgd-xi/deep-wine-runner  
Github：https://github.com/gfdgd-xi/deep-wine-runner  
Gitlink：https://www.gitlink.org.cn/gfdgd_xi/deep-wine-runner  
蓝奏云：https://gfdgdxi.lanzouj.com/b01nz7y3e，密码:7oii  
星火应用商店：spk://store/tools/spark-deepin-wine-runner  

## 更多
+ https://gitee.com/gfdgd-xi/deep-wine-runner
+ https://github.com/gfdgd-xi/deep-wine-runner
+ https://www.gitlink.org.cn/gfdgd_xi/deep-wine-runner

## 程序下载量
![](https://gfdgd-xi.github.io/images/wine-runner.svg)  

## Star 一下吧
开发不易，原创艰难，给一个 Star 吧，你的 Star 是我继续开发的动力  
[![star](https://gitee.com/gfdgd-xi/deep-wine-runner/badge/star.svg?theme=dark)](https://gitee.com/gfdgd-xi/deep-wine-runner/stargazers)

# ©2020-Now