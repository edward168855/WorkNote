#App签名


###APP系统签名

具体步骤是下载：platform.pk8、platform.x509.pem、signapk.jar三个文件，建议放在同一个目录下
准备好上述文件以后，编写一个批处理文件放在同一个目录下
批处理文件的创建很简单，先创建一个TXT文件，写好以后把后缀名改为.bat就可以了
批处理文件中写以下内容：
va -jar signapk.jar platform.x509.pem platform.pk8  原文件名.apk 目标文件名.apk
adb remount
adb push MyDemo_signed.apk  /system/app
pause
批处理文件的名字随便取

运行批处理文件后，我们的程序就自动运行在设备上了。
这里要注意，只有在debug模式下我们才能这样处理。

对了，这里提一句，系统签名并且运行的时候，一定要把项目里的so文件全部push到系统app文件夹下啊
>引用[系统签名](http://blog.csdn.net/u011791526/article/details/52151130)


###APP系统签名命令（如果不想用批处理的话）

 java -jar signapk.jar  platform.x509.pem   platform.pk8 old.apk new.apk

举例如下:
java -jar D:\2017\02\06\debug_sign_key\signapk.jar D:\2017\02\06\debug_sign_key\platform.x509.pem D:\2017\02\06\debug_sign_key\platform.pk8 C:\Users\sky90\Desktop\DesktopForCommon.apk C:\Users\sky90\Desktop\signed.apk


![资源放置位置](http://t3.qpic.cn/mblogpic/c27407de90facb438550/460)