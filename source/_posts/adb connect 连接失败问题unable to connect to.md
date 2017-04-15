---
title: adb connect 连接失败问题unable to connect to
date: 2016-10-05 10:02:27
tags: 
- adb
- 调试
categories: 
- android开发
comment: true
---

### android手机下载WIFI ADB和终端模拟器（需root手机）

 1. 打开WIFI ADB  
 ![wifi adb](http://img.blog.csdn.net/20161005091627846)
 2. 执行 adb connect 192.138.30.143:5555  
 结果**失败**了  
 ![连接失败](http://img.blog.csdn.net/20161005092321610)
 3. 上网搜解决方案  
 参考方案：http://blog.csdn.net/banith78/article/details/18595163
 4. 在android手机上打开终端模拟器依次输入以下命令  
 >su
 >setprop service.adb.tcp.port 5555
 >stop adbd
 >start adbd  
 
 截图：![截图](http://img.blog.csdn.net/20161005093124160)  
 **确保手机root后，且给终端模拟器root权限后在执行以上命令，不然是会失败的。**
 5. 最终连接成功  
 ![这里写图片描述](http://img.blog.csdn.net/20161005093832034)

###总结
我在网上看到了有的人直接打开wifi adb，直接连接就能成功（有root权限），但是我也有root权限，也进行授权了，就是连接失败，可能和MIUI有关吧。

**另外**我在github上搜到了一个关于wifiadb的源码（不确定是我用的那个软件，但原理肯定大致一样）
```java
protected static int set(int paramInt) throws IOException,
			InterruptedException {
		Process localProcess = Runtime.getRuntime().exec("su");
		DataOutputStream localDataOutputStream = new DataOutputStream(
				(OutputStream) localProcess.getOutputStream());
		localDataOutputStream.writeBytes("setprop service.adb.tcp.port "
				+ paramInt + "\n");
		localDataOutputStream.flush();
		localDataOutputStream.writeBytes("stop adbd\n");
		localDataOutputStream.flush();
		localDataOutputStream.writeBytes("start adbd\n");
		localDataOutputStream.flush();
		localDataOutputStream.writeBytes("exit\n");
		localDataOutputStream.flush();
		localProcess.waitFor();
		return localProcess.exitValue();
	}
```
按道理程序执行的代码就应该能正确连接成功的，还是让我折腾了一圈。
希望能对你有一点帮助！
