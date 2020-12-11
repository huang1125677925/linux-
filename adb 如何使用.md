## 电脑和手机的连接

- 打开Android手机的USB调试模式，并连接到MAC电脑
- 使用命令【adb devices】查看已连接的手机，如果找不到，则：
- 使用命令【system_profiler SPUSBDataType】查看手机的VID，并将VID写入到~/.android/adb_usb.ini文件中，该文件可能需要新建。
- 使用命令【adb kill-server】停止服务，并使用命令【adb start-server】重启服务
- 再次执行【adb devices】查看已连接的手机。



## Adb 常用命令

- 查看ADB版本：adb version
- 查看手机设备：adb devices
- 查看设备型号：adb shell getprop ro.product.model
- 查看电池信息：adb shell dumpsys battery
- 查看设备ID：adb shell settings get secure android_id
- 查看设备IMEI：adb shell dumpsys iphonesubinfo
- 查看Android版本：adb shell getprop ro.build.version.release
- 查看手机网络信息：adb shell ifconfig
- 查看设备日志：adb logcat
- 重启手机设备：adb reboot
- 安装一个apk：adb install /path/demo.apk
- 卸载一个apk：adb uninstall <package>
- 查看系统运行进程：adb shell ps
- 查看系统磁盘情况：adb shell ls /path/
- 手机设备截屏：adb shell screencap -p /sdcard/aa.png
- 手机文件下载到电脑：adb pull /sdcard/aa.png ./
- 电脑文件上传到手机：adb push aa.png /data/local/
- 手机设备录像：adb shell screenrecord /sdcard/ab.mp4
- 手机屏幕分辨率：adb shell wm size
- 手机屏幕密度：adb shell wm density
- 手机屏幕点击：adb shell input tap xvalue yvalue
- 手机屏幕滑动：adb shell input swipe 1000 1500 200 200
- 手机屏幕带时间滑动：adb shell input swipe 1000 1500 0 0 1000
- 手机文本输入：adb shell input text xxxxx
- 手机键盘事件：adb shell input keyevent xx
- 连接多个手机设备时，指定手机设备：adb -s serialNumber <command>