## 需要了解自己手机的cpu是什么指令集

了解是什么指令集最好的办法还是通过去相对权威的网站来看cpu所对应的指令集

然后下载相对应的busybox安装包

 http://www.busybox.net/downloads/binaries 



## 把这个busybox文件给迁移到指令目录下

```
adb push busybox /system/xbin
```





## 安装这个busybox，在root下进行安装

```
su
chmod 755 busybox 
#/system/xbin 下
busybox --install .
```



## 问题解决

### 在adb shell下安装时说没有文件只读

这是因为/  system这个下边的几个文件（具体我也不知道范围），只能读

所以需要先修改其文件读写权限，然后才能够进行install



按理说只要有了root权限，改这些都是小意思

```
mount -o rw,remount /
mount -o ro,remount /
```



实际上这个mount命令，我不是太熟悉，总之这样就可以了