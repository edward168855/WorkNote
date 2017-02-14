#adb常用命令

###adb命令查询盒子IP
adb shell ip a
或者 用adb shell netcfg
![示例图片](https://github.com/edward168855/WorkNote/blob/master/app/src/main/java/com/lpf/worknote/summary/cmd/4baa56e5-9ec3-4045-9198-b466d7c20588.png?raw=true)

###adb 常用命令行

一、启动activity

adb shell am start -n  com.clt.vpntest/.MainActivity

二、重签名

20151211 使用命名如下：

C:\Users\Think>java -jar D:\qianming\signapk.jar  D:\qianming\security\platform.x509.pem D:\qianming\security\platform.pk8 D:\files\VpnTest2\app\build
\outputs\apk\app-release-unsigned.apk D:\qianming\VpnTest.apk

注意：
复制使用这个命名的时候，注意换行时候的空格

三、生成debugkeystore文件

20151211 我用的时候写的命令如下：

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






























