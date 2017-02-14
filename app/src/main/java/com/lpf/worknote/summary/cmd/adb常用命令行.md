#adb常用命令

###adb命令查询盒子IP
adb shell ip a
或者 用adb shell netcfg
![示例图片](https://github.com/edward168855/WorkNote/blob/master/app/src/main/res/mipmap-hdpi/4baa56e5-9ec3-4045-9198-b466d7c20588.png?raw=true)

###adb 常用命令行


####**_20151209总结_**

一、查看里面所有文件包名
adb shell
pm list packages -d

根据包名来disable、enable一个程序：
adb shell
pm list packages -d
pm disable com.hexun.fund

pm enable com.hexun.fund

二、查找设备时的操作
插上电源，连接网线，然后用colordebug
ping 192.168.1.109

adb connect 192.168.1.109

adb devices

如果连接不上，就重启一下（拔掉电源，然后再接上电源）


三、push 一个文件到指定文件夹的时候采用如下命令

adb remount

adb push D:\files\base.apk /system/priv-app

当adb push *.apk /system/app的时候出现Read-only file system的时候使用命令adb shell mount -o remount rw /system

四、查看里面所有的文件夹方法

adb shell
mount

五、用命令startActivity进行升级的命令
adb shell am start  -n  android.rockchip.update.service/.UpdateAndRebootActivity  --es android.rockchip.update.extra.IMAGE_PATH /mnt/sdcard/update/update.zip

六、根据包名查看一个apk的permission及其他信息
adb shell dumpsys package com.color.info

七、 用命令行开启一个app，（其中com.clt.vpntest为app包名，在AndroidMenifest.xml中）
adb shell am start -n  com.clt.vpntest/.MainActivity

八、 查找包含“vpn字符的apk及它的包名” adb shell pm list packages -f | grep vpn

九、启动一个Service  :   am startservice -n com.clt.activity.mictesttwo/com.clt.activity.mictesttwo.MyService

十、从Logcat 中获取特定日志信息（比如含vpn字段的）adb logcat | grep vpn

十一、查询盒子当中IP的命令：adb shell ip a 或者用 adb shell netcfg

十二、根据包名来查询一个apk的信息 dumpsys
adb shell dumpsys package com.clt.vpntest | more
十三、把apk命名成指定的名称并放到指定文件目录下
adb push E:\Android\AndroidStudioProjects\VpnTest\app\build\outputs\apk\app-debug.apk /system/priv-app/VpnTest.apk
十四、查询package当中的信息
adb dumpsys package
十五、查询logcat当中的含有指定字符的信息（比如下面这个unlock）
adb logcat | grep unlock
十六、查询盒子当中指定目录所包含的所有内容
adb shell ls -l /system/priv-app/
十七、把查询到的盒子里面所有包的信息写到packages.txt文件当中
adb shell dumpsys package > packages.txt
十八、查询盒子里面所有包的更多信息
adb shell dumpsys package | more
十九、查询盒子里面所有包含“1001”字符的所有包的信息
adb shell dumpsys package | grep 1001
二十、查询盒子里面所有包含“com.clt.vpntest”字段的包
adb shell dumpsys package com.clt.vpntest
二十一、同“二十”
adb shell dumpsys package com.android.settings
二十二、在指定文件夹当中查找包含特定字符的文件（比如下面这两个命令）
D:\VPN>grep "Type the password" * -r
D:\VPN>grep credentials_unlock_hint * -r
二十三、查询所以包名中包含特定字符的包（比如下面查询这个包含“vpn”字符的包名）
adb shell pm list packages -f | grep vpn



####**_20151211总结_**

一、启动activity

adb shell am start -n  com.clt.vpntest/.MainActivity

二、重签名

使用命名如下：

C:\Users\Think>java -jar D:\qianming\signapk.jar  D:\qianming\security\platform.x509.pem D:\qianming\security\platform.pk8 D:\files\VpnTest2\app\build
\outputs\apk\app-release-unsigned.apk D:\qianming\VpnTest.apk

注意：
复制使用这个命名的时候，注意换行时候的空格

三、生成debugkeystore文件

我用的时候写的命令如下：

C:\Users\Think>openssl pkcs8 -in D:\qianming\security\platform.pk8 -inform DER -outform PEM -out D:\qianming\shared.priv.pem -nocrypt

C:\Users\Think>openssl pkcs12 -export -in D:\qianming\security\platform.x509.pem -inkey D:\qianming\shared.priv.pem -out D:\qianming\shared.pk12 -name
 androiddebugkey
Loading 'screen' into random state - done
Enter Export Password:
Verifying - Enter Export Password:

C:\Users\Think>keytool -importkeystore -deststorepass android -destkeypass android -destkeystore D:\qianming\debug.keystore -srckeystore D:\qianming\s
hared.pk12 -srcstoretype PKCS12 -srcstorepass android -alias androiddebugkey

注意：
复制上面命令直接使用的时候注意其中存在的空格 。

四、验证签名是否正确
jarsigner -verify -verbose -certs D:\qianming\VpnTest.apk

五、查找vpn的apk
adb shell pm list packages -f | grep vpn

注意：
apk push到系统之后要重启一下系统才能生效。
android自带的usb驱动在它的sdk目录下。



####20170214总结
























