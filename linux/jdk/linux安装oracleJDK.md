## linux 安装oracle JDK：
#### 1. 卸载openJDK：
* 已安装openjdk
 yum install java-1.8.0-openjdk.i686

* 卸载:
 yum -y remove java-1.8.0-openjdk.i686

#### 2. 安装oracle jdk
 * 在 oracle网站下载32位的[JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

 * 上传到远程服务器并解压
 `tar -vxf jdk-8u121-linux-i586.tar.gz`
 `cd jdk1.8.0_121`

 * 移动jdk1.8.0_121
  `mv jdk1.8.0_121/ /usr/local`

 * 设置java环境 /etc/profile
在/etc/profile文件最后添加
```
export JAVA_HOME=/usr/local/jdk1.8.0_121
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```
 * 运行文件 /etc/profile

 `. /etc/profile`中间有空格
