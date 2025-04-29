# java

javac java javap

$ javac HelloWorld.java
$ java HelloWorld
Hello World

java -> .class -JVM-->
其实JVM运行的不是java，而是class（字节码）
理论上其他语言也可以转换为class由JVM运行
这是JAVA跨平台的关键

linux安装

```bash
sudo apt update
sudo apt install default-jdk
sudo apt install default-jre
```

java -version