## JavaPoetTest

简介： 当项目中同时存在android项目和java项目时，java项目中引用的库无法正常依赖。而只有java项目存在时，则可以正常依赖。该项目通过两种方案来临时解决这种不能正常依赖的问题。如果需要根除，目前只能让java项目单独为一个工程。

```java
/home/su/App/android-studio/jre/bin/java -javaagent:/home/su/App/android-studio/lib/idea_rt.jar=33373:/home/su/App/android-studio/bin -Dfile.encoding=UTF-8 -classpath /home/su/桌面/tmp/SimpleTest/javapoet/build/classes/java/main:/home/su/App/android-studio/jre/jre/lib/charsets.jar:/home/su/App/android-studio/jre/jre/lib/ext/cldrdata.jar:/home/su/App/android-studio/jre/jre/lib/ext/dnsns.jar:/home/su/App/android-studio/jre/jre/lib/ext/jaccess.jar:/home/su/App/android-studio/jre/jre/lib/ext/localedata.jar:/home/su/App/android-studio/jre/jre/lib/ext/nashorn.jar:/home/su/App/android-studio/jre/jre/lib/ext/sunec.jar:/home/su/App/android-studio/jre/jre/lib/ext/sunjce_provider.jar:/home/su/App/android-studio/jre/jre/lib/ext/sunpkcs11.jar:/home/su/App/android-studio/jre/jre/lib/ext/zipfs.jar:/home/su/App/android-studio/jre/jre/lib/jce.jar:/home/su/App/android-studio/jre/jre/lib/jsse.jar:/home/su/App/android-studio/jre/jre/lib/management-agent.jar:/home/su/App/android-studio/jre/jre/lib/resources.jar:/home/su/App/android-studio/jre/jre/lib/rt.jar tv.lycam.javapoet.JavaPoet
Exception in thread "main" java.lang.NoClassDefFoundError: com/squareup/javapoet/MethodSpec
	at tv.lycam.javapoet.JavaPoet.main(JavaPoet.java:13)
Caused by: java.lang.ClassNotFoundException: com.squareup.javapoet.MethodSpec
	at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:331)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 1 more
```

### 第一种方案

- 每次sync都需要这样修改一次

* 打开模块目录下的.iml文件

* 找到orderEntry中javapoet的依赖，做如下修改

```xml
<orderEntry type="library" exported="" scope="PROVIDED" name="javapoet" level="project"/>
```

修改后（去掉scope）

```xml
<orderEntry type="library" exported="" name="javapoet" level="project"/>
```

* 修改后不要同步，直接运行main方法即可

### 第二种方案

- 每次sync都需要这样执行一次

* 在模块中的`build.gradle`中添加`apply plugin: 'idea'`

* 控制台执行命令`gradle idea`后运行main方法


