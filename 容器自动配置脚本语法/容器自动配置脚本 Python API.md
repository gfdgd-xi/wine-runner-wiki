# 容器自动配置脚本 Python API
## 建议先阅读
因为这个 Python API 是在之前的脚本语法旧引擎和 Bash 引擎的基础上制作的，所以建议先阅读前面的旧引擎和 Bash 引擎的文档  
### API 要求
1. Linux 环境，需要安装 Python（≥3.6.0）
2. 安装 Wine 运行器（≥2.4.0）
## 调用方法
在安装 Wine 运行器（≥2.4.0）后，在默认 Python 环境输入：
```python
import WineRunner
```
即可
## 方法（类）介绍
| 类名称 | 用途 | 参数 |
| :-: | :-: | :-: |
| `WineRunner.Old()` | 调用旧版的脚本解释引擎 | `(wine: str -> 需要调用的Wine, wineprefix: str -> 需要指定运行的容器名)` |
| `WineRunner.Bash()` | 调用基于 Bash 的脚本解释引擎 | `(wine: str -> 需要调用的Wine, wineprefix: str -> 需要指定运行的容器名)` |
| `WineRunner.programPath: str` | 解释器所在路径 |
### Old 类内函数/变量解释
| 函数 | 用途 |
| :-: | :-: |
| `WineRunner.Old().runCommand(command: str -> 命令)` | 使用旧版的解析引擎运行指定命令（命令传入为字符串形式） |
| `WineRunner.Old().runList(command: list -> 命令)` | 使用旧版的解析引擎运行指定命令（命令传入为数组形式），数组格式如下：`[["bat", "winver"]]` |
| `wine: str` | 调用的 Wine |
| `wineprefix: str` | 调用的 Wine 容器 |
#### 数组示例（WineRunner.Old.runList的command参数）
```json
[
    ["bat", "winver"],
    ["bash", "ls"],
    ["pause"]
]
```
### Bash 类内函数解释
| 函数 | 用途 |
| :-: | :-: |
| `WineRunner.Bash().runCommand(command: str -> 命令)` | 使用基于 Bash 的解析引擎运行指定命令（命令传入为字符串形式） |
| `WineRunner.Bash().runList(command: list -> 命令)` | 使用基于 Bash 的解析引擎运行指定命令（命令传入为数组形式），数组格式如下：`[["bat", "winver"]]` |
| `wine: str` | 调用的 Wine |
| `wineprefix: str` | 调用的 Wine 容器 |
#### 数组示例（WineRunner.Bash.runList的command参数）
```json
[
    ["bat", "winver"],
    ["ls"],
    ["pause"]
]
```
## Demo
### 原 Bash 版
```bash
#!/usr/bin/env deepin-wine-runner-auto-install-bash
# 使用 Wine 运行器的 Bash 解释器运行
#################################################################################################################
# 作者：gfdgd xi
# 版本：2.4.0
# 更新时间：2022年10月30日
# 基于 Wine 运行器
###############################################################################################
# 用于判断是否为 bash 解释器
# 旧版解释器直接提示不兼容
if [[ 1 == 2 ]]; then
    error 错误 此脚本只支持\ Wine\ 运行器\ 2.3.0\ 及以上版本，请更新至最新版本
    exit
fi
# 操作
echo Power By $MAKER
echo $COPYRIGHT
rm -rfv /tmp/firefox.exe
download https://download-origin.cdn.mozilla.net/pub/firefox/releases/105.0.2/win32/zh-CN/Firefox%20Setup%20105.0.2.exe?gfdgd-xi /tmp firefox.exe
bat reg add 'HKEY_USERS\S-1-5-21-0-0-0-1000\Software\Wine\X11 Driver' /v Decorated /d N /f
bat /tmp/firefox.exe
info 提示 安装完成！
```
### Python 版情况1
```python
#!/usr/bin/env python3
# 使用系统默认的 python3 运行
#################################################################################################################
# 作者：gfdgd xi
# 版本：2.4.0
# 更新时间：2022年10月30日
# 基于 Wine 运行器
#################################################################################################################
#################
# 引入所需的库
#################
import WineRunner
for i in """echo Power By $MAKER
echo $COPYRIGHT
rm -rfv /tmp/firefox.exe
download https://download-origin.cdn.mozilla.net/pub/firefox/releases/105.0.2/win32/zh-CN/Firefox%20Setup%20105.0.2.exe?gfdgd-xi /tmp firefox.exe
bat reg add 'HKEY_USERS\S-1-5-21-0-0-0-1000\Software\Wine\X11 Driver' /v Decorated /d N /f
bat /tmp/firefox.exe
info 提示 安装完成！""".splitlines():
    WineRunner.Bash().runCommand(i)
```
### Python 版情况 2
```python
#!/usr/bin/env python3
# 使用系统默认的 python3 运行
#################################################################################################################
# 作者：gfdgd xi
# 版本：2.4.0
# 更新时间：2022年10月30日
# 基于 Wine 运行器
#################################################################################################################
#################
# 引入所需的库
#################
import WineRunner
WineRunner.Bash().runList([
    ["echo", "Power By $MAKER"],
    ["echo", "$COPYRIGHT"],
    ["rm", "-rfv", "/tmp/firefox.exe"],
    ["download", "https://download-origin.cdn.mozilla.net/pub/firefox/releases/105.0.2/win32/zh-CN/Firefox%20Setup%20105.0.2.exe?gfdgd-xi", "/tmp", "firefox.exe"],
    ["bat", "reg", "add", "HKEY_USERS\S-1-5-21-0-0-0-1000\Software\Wine\X11 Driver", "/v", "Decorated", "/d", "N", "/f"],
    ["bat", "/tmp/firefox.exe"],
    ["info", "提示", "安装完成"]
])

```