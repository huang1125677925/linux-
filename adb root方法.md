## 解决adbd cannot run as root in production builds问题

版权

1，验证你的手机是否已经root了

adb shell

su

行命令后，$ 变为 # 即 表示root 成功

2，安装adbd-insecure.apk

adb install adbd-insecure.apk

3，设置

打开应用将Enable insecure adbd 和 enable at boot 勾选上，设置好之后重进键入：adb root即可

[参考文章](https://blog.csdn.net/hlllmr1314/article/details/52217128)