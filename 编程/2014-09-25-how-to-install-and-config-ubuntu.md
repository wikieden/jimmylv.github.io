---
layout: post
title: 'Ubuntu系统的安装与优化'
category: 编程
tags: [Ubuntu, OS]
published: true
---

## 安装 Ubuntu

[参考教程](http://jingyan.baidu.com/article/ff42efa9423991c19e22020d.html)

### 1. Win 下的准备：

- [下载.iso 文件](http://www.ubuntu.com/download/desktop)
- [UltraISO 下载](http://www.baidu.com/s?&wd=UltraISO)
- [制作 U 盘启动器](http://jingyan.baidu.com/article/d169e186800f02436711d87b.html)
- 修改 BIOS 设置为 U 盘启动：HP 电脑开机按 F9

### 2. 安装中的分区问题：

- swap: 交换空间，类似于 Win 下的虚拟空间。（内存够大也许不需要）
- /: 根目录，系统的安装目录，相当于 C 盘，重装时数据丢失。
- /boot 是开机引导系统用的，建立此分区可使 Win 引导 Ubuntu，否则默认 Ubuntu 引导 Win。
- /home 是个人资料文件夹（下载/音乐/文档）这些，重装时数据保留。

### 3. 安装过程中下载软件更新和安装软件部分可以 skip

## Ubuntu 软件

### 1. 简化安装：Synaptic (新立得)

- 是 Ubuntu 的包管理工具 apt 的图形化前端。
- 集成了很多一键安装的软件包，eg: LAMP 解决包依赖的问题。
- 这里可以先在系统 Software Center 内安装这个软件
- tips: 注意此软件打开时 terminal 中无法使用 apt-get

```bash
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```

### 2. 词典：Youdao/Stardict/GoldenDict

- 星际词王最容易安装和使用。

- [Ubuntu-youdao](https://www.google.com/search?q=Ubuntu-youdao)安装不上。

- [GoldenDict](https://www.google.com/search?q=GoldenDict)配置太麻烦。

### 3. 输入法：搜狗/Google 输入法（Fcitx 系列）

- 在 synaptic 中搜索*googlepinyin*即可安装

### 4. 浏览器：Firefox/Chromium

- 还未安装 Chromium 时使用火狐，火狐的 flash 插件可以在软件商店中心下载安装解决

- 解决 google 无法访问 [参考知乎](http://www.zhihu.com/question/21245060/answer/27201877)

> 1. 修改 DNS/host：更改系统文件，可能出现莫名奇妙的问题
> 2. GoAgent + [SwitchySharp](http://www.baidu.com/s?&wd=SwitchySharp)：GoAgent 不稳定
> 3. [红杏](http://botey.cn/UPLOAD/All_Files/Chrome_Red.rar)：付费，但是基础功能提高 Google 的访问，足以。
>    tips：此时都不能从 Google 应用商店下载，只能先下载再拖入 chromium 安装

- 解决 flash
  Pepper Flash Player，一个来自 Google 更安全更稳定的版本的 Flash Player

```bash
sudo apt-get install pepperflashplugin-nonfree
sudo update-pepperflashplugin-nonfree --install
```

### 5. 系统优化：[Ubuntu Tweak](http://ubuntu-tweak.com/)

- 国人 TualatriX 开发的 ubuntu 平台下的优化大师，简单易用

- 可以设置字体/清理垃圾/查看软件

### 6. 下拉式终端：「[Guake Terminal](https://github.com/Guake/guake/)」

- `sudo apt-get build-dep guake`

## 界面美化/优化

### 1. 鼠标指针闪烁

- [关闭 “未知显示器”](http://jingyan.baidu.com/article/3aed632e78668970108091c0.html)

### 2. 在当前目录打开 terminal

```bash
sudo apt-get install nautilus-open-terminal
#reload dir
nautilus -q
```

### 3. 字体/语言

- 系统语言使用 English，默认字体看起来就很舒服

- 浏览器中的字体实在太难看，下载[微软雅黑字体](http://www.baidu.com/s?&wd=微软雅黑字体) -> 在浏览器中选择相应字体+chrome 扩展

### 4. 使用开源字体库文泉驿的微黑字体

1. 安装文泉驿微黑字体库

```sh
sudo apt-get install ttf-wqy-microhei
```

2. 下载安装[Ubuntu Tweak](http://ubuntu-tweak.com/)

原系统设置中没有找到修改字体的地方，使用 Ubuntu Tweak：调整－>字库中，将默认字体、桌面字体等做修改

![](https://raw.staticdn.net/JimmyLv/images/master/images/2016/1487949759355.png)

3. 进一步确认并修改字体配置文件

> - 通常 Ubuntu 的字体文件存放在/usr/share/fonts 下面，字体配置配置文件放在/etc/fonts 下面
> - Ubuntu 对中文字体的控制集中在一个文件/etc/fonts/conf.d/69-language-selector-zh-cn.conf
> - 编辑文件：`sudo gedit /etc/fonts/conf.d/69-language-selector-zh-cn.conf`

修改如下：

```html
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="pattern">
    <test name="lang">
      <string>zh-cn</string>
    </test>
    <test qual="any" name="family">
      <string>serif</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>WenQuanYi Micro Hei</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL New Sung</string>
      <string>WenQuanYi Bitmap Song</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
      <string>HYSong</string>
    </edit>
  </match>
  <match target="pattern">
    <test qual="any" name="family">
      <string>sans-serif</string>
    </test>
    <test name="lang">
      <string>zh-cn</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>WenQuanYi Micro Hei</string>
      <string>Droid Sans Fallback</string>
      <string>HYSong</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL New Sung</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
    </edit>
  </match>
  <match target="pattern">
    <test qual="any" name="family">
      <string>monospace</string>
    </test>
    <test name="lang">
      <string>zh-cn</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>WenQuanYi Micro Hei Mono</string>
      <string>Droid Sans Fallback</string>
      <string>HYSong</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL New Sung</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
    </edit>
  </match>
</fontconfig>
```
