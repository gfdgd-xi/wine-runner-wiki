# 使用Qemu User运行Wine（支持全架构）
## 提醒
Qemu 的转换效率较低，如果可以的话建议使用其它方案以提升运行效率  
此方案理论上支持全架构（**amd64、arm64、mips64、loongarch64、riscv64、ppc64、s390x……**），只要能跑 Qemu User 即可，在 x86、arm64 真机测试通过  
Wine 运行器版本要求：≥3.2.0  
### 一个坑
下面提供的运行环境安装包会与其它运行库/其它跨架构翻译软件冲突，如果发生冲突可以移除掉对应的运行环境安装包  
如安装 box86/64、exagear、lat 可能会与 amd64/i386 运行环境安装包冲突  

## 使用 Wine 运行器搭建环境
1. 先安装 Qemu User  
  ![图片.png](https://storage.deepin.org/thread/202304161949507685_图片.png)

2. 安装 i386 + amd64 运行库  
  ![图片.png](https://storage.deepin.org/thread/202304161951332720_图片.png)  
  ![图片.png](https://storage.deepin.org/thread/202304161950523796_图片.png)  

3. 安装 Wine  
  ![图片.png](https://storage.deepin.org/thread/202304161952268343_图片.png)  
  ![图片.png](https://storage.deepin.org/thread/202304161953003245_图片.png)  
  （选择需要的 Wine 安装）

然后按照正常使用 Wine 的方法使用即可

### 常见问题
#### 安装运行库时出现以下提示
> ![图片.png](https://storage.deepin.org/thread/202304162027211739_图片.png)  
代表您已经安装了对应架构的运行库，不需要再另外安装了  

## 手动搭建环境
### 安装 Qemu User
```bash
sudo apt install binfmt-support qemu-user qemu-user-static -y
```
### 安装运行库
| 架构 | 运行库下载 |
|-|-|
| i386 | https://code.gitlink.org.cn/gfdgd_xi/runtime-for-qemu/raw/branch/master/i386-runtime-for-qemu_1.0.0_all.deb |
| amd64 | https://code.gitlink.org.cn/gfdgd_xi/runtime-for-qemu/raw/branch/master/amd64-runtime-for-qemu_1.0.0_all.deb |



# ©2020~2023 gfdgd xi