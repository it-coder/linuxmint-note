# linuxmint-note
> 准备入linux的坑，先在虚拟机中折腾，记录下使用心得和技巧！


### 个人环境

+ linux mint 19.2
+ [资源地址](https://mirrors.tuna.tsinghua.edu.cn/linuxmint-cd/stable/19.2/)


### 常用开发命令

``` shell
apt-cache search package #搜索包
sudo apt-get -f install #修复安装"-f = --fix-missing"
sudo apt-get remove package # 删除包
sudo apt-get remove package --purge #删除包，包括删除配置文件等
sudo apt-get dist-upgrade #升级系统
sudo apt-get clean && sudo apt-get autoclean #清理无用的包

#系统apt安装的软件包通常都是下载到如下文件夹：
#/var/cache/apt
```

### 安装输入法

+ 需要安装使用fcitx框架
+ 下载安装搜狗输入法
``` shell
sudo wget http://cdn2.ime.sogou.com/dl/index/1571302197/sogoupinyin_2.3.1.0112_amd64.deb?st=FB5F9AtdR58j1bisQL2chQ&e=1575878906&fn=sogoupinyin_2.3.1.0112_amd64.deb

sudo apt-get install ~/${path}/sogoupinyin_2.3.1.0112_amd64.deb
```

+ 解决文字颜色淡的问题
```
sudo apt-get install language-selector-*
sync
reboot
```

### 微信安装

参考[资料](https://forum.ubuntu.org.cn/viewtopic.php?f=73&p=3217021&sid=6194a64cefc1f4c5ac43dcd8729ca3c8)

整理如下脚本(下载的版本需要根据实际情况来：例如: deepin-wine_2.18-12 升级为 deepin-wine_2.18-22~rc0)
``` shell
mkdir /tmp/deepintemp
cd /tmp/deepintemp
# 下载
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/deepin-wine_2.18-22~rc0_all.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/deepin-wine32_2.18-22~rc0_i386.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/deepin-wine32-preloader_2.18-22~rc0_i386.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine-helper/deepin-wine-helper_1.2deepin8_i386.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine-plugin/deepin-wine-plugin_1.0deepin2_amd64.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine-plugin-virtual/deepin-wine-plugin-virtual_1.0deepin3_all.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine-uninstaller/deepin-wine-uninstaller_0.1deepin2_i386.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/u/udis86/udis86_1.72-2_i386.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/deepin-fonts-wine_2.18-22~rc0_all.deb
wget http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/deepin-libwine_2.18-22~rc0_i386.deb
wget https://mirrors.aliyun.com/deepin/pool/main/libj/libjpeg-turbo/libjpeg62-turbo_1.5.1-2_amd64.deb
wget https://mirrors.aliyun.com/deepin/pool/main/libj/libjpeg-turbo/libjpeg62-turbo_1.5.1-2_i386.deb

# 安装
echo '准备添加32位支持'
sudo dpkg --add-architecture i386
echo '添加成功，准备刷新apt缓存信息...'
sudo apt update
echo '即将开始安装...'
sudo dpkg -i *.deb
echo '安装完成，正在自动安装依赖...'
sudo apt install -fy

# 删除已下载资源包
rm -vfr /tmp/deepintemp

# 然后下载安装微信等window工具
sudo apt-get install ./deepin.com.wechat_2.6.8.65deepin0_i386.deb    
```
+ [deepin软件资源地址](http://mirrors.aliyun.com/deepin/pool/non-free/d/)
+ [deepin框架资源下载地址](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin-wine/)

> 原github的deepin-wine-ubututu项目因有一年未维护所以无法安装成功了.
> 根据教程下载安装最新版本的deepin-wine框架 然后再安装微信等聊天工具

### jdk开发环境

+ 下载jdk1.8
+ 配置
> 用户级别：`./.bashrc`，系统级别： `/etc/profile`
``` shell
export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_131    # 你的 JDK 解压路径
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

# 刷新
source ~/.bashrc
# 或 source /etc/profile
```

