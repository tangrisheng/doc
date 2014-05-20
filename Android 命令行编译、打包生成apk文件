Android 命令行编译、打包生成apk文件
==========================================

# 一、搭建搭建环境
1. 安装JDK 和 Android SDK
2. 配置环境变量 
D:\android-sdk-windows\tools 
C:\Program Files\Java\jdk1.6.0_20\bin 
3. 例子信息 
项目目录：D:\ProjectDemo 
SDK目录 ：D:\android-sdk-windows\platforms\android-8\ 
# 二、命令行编译Android项目
1. 生成R文件
2. Java代码生成class文件
3. class文件生成dex文件
4. 打包资源
5. 生成apk
6. 创建密匙
7. 签名apk
## 1. aapt命令， 生成R文件 
<pre>
> aapt package -f -m -J ./gen -S res -M AndroidManifest.xml -I D:\android.jar
</pre>
-f 如果编译生成的文件已经存在，强制覆盖。 
-m 使生成的包的目录存放在-J参数指定的目录 
-J 指定生成的R.java 的输出目录路径 
-S 指定res文件夹的路径
-I 指定某个版本平台的android.jar文件的路径
-A 指定assert文件夹的路径
## 2. javac命令，生成class文件 
<pre>
> javac -target 1.5 -bootclasspath D:\android-sdk-windows\platforms\android-8\android.jar -d bin src\demo\project\*.java gen\demo\project\R.java
</pre>
  -target <版本>               生成特定 VM 版本的类文件 
  -bootclasspath <路径>        覆盖引导类文件的位置 
  -d <目录>                    指定存放生成的类文件的位置 
  -sourcepath <路径>           指定查找输入源文件的位置 

## 3. dx 命令，把class文件转换为.dex文件 
<pre>
> dx --dex --output=D:\ProjectDemo\bin\classes.dex D:\ProjectDemo\bin
</pre>
--output=<要生成的classes.dex路径> <要处理的class文件的路径> 

## 4. aapt命令，打包资源 
<pre>
> aapt package -f -M AndroidManifest.xml -S res -I D:\android-sdk-windows\platforms\android-8\android.jar -F bin\resources.ap_
</pre>
-f 如果编译生成的文件已经存在，强制覆盖 
-M 指定AndroidManifest.xml的路径 
-S 指定res文件夹路径
-I 指定某个版本平台的android.jar的路径
-F 指定输出文件完整路径
## 5. apkbuilder命令，生成apk 
<pre>
> apkbuilder D:\ProjectDemo\bin\projectdemo.apk -v -u -z D:\ProjectDemo\bin\resources.ap_ -f D:\ProjectDemo\bin\classes.dex -rf D:\ProjectDemo\src
</pre>

-v Verbose 显示过程信息 
-u 创建一个无签名的包 
-z 指定apk资源路径 
-f 指定dex文件路径
-rf 指定源码路径
## 6. 创建密钥 
<pre>
> keytool -genkey -alias release -keyalg RSA -validity 20000 -keystore release.keystore
</pre>
-genkey      在用户主目录中创建一个默认文件".keystore",还会产生一个mykey的别名，mykey中包含用户的公钥、私钥和证书 
-alias       产生别名 
-keyalg      指定密钥的算法  
-validity    指定创建的证书有效期多少天 
-keystore    指定密钥库的名称(产生的各类信息将不在.keystore文件中) 

## 7. 签名 
<pre>
> jarsigner  -verbose -keystore C:\Users\UserName\Desktop\build\release.keystore -storepass antmima -keypass antmima -signedjar D:\ProjectDemo\bin\projectdemo-signed.apk D:\ProjectDemo\bin\projectdemo.apk release
</pre>
-verbose  签名/验证时输出详细信息 
-keystore 密钥库位置 
-storepass          用于密钥库完整性的口令 
-keypass            专用密钥的口令（如果不同） 
-signedjar          已签名的 JAR 文件的名称 （第一个apk是签名之后的文件， 第二个apk是需要签名的文件）
