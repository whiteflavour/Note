# Gradle

## 换源、代理：

### 换源：

C 盘 .gradle 文件夹下 -> 创建 init.gradle 文件：

init.gradle: 

```groovy
allprojects {  
   repositories {  
       maven {  
           url "https://maven.aliyun.com/repository/public"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/jcenter"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/spring"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/spring-plugin"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/gradle-plugin"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/google"  
       }  
       maven {  
           url "https://maven.aliyun.com/repository/grails-core"  
       } 
       maven {  
           url "https://maven.aliyun.com/repository/apache-snapshots"  
       }  
   }  
} 
```

### 代理（推荐）：★

开启全局代理，因为 Gradle 非常灵活，所以有些脚本可能依赖于 github 或者其他地方的远程脚本。

.gradle 文件夹下 -> 新建 gradle.properties 文件：

gradle.properties：

```properties
# org.gradle.jvmargs=-Xmx4g -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8  
systemProp.http.proxyHost=127.0.0.1  
systemProp.http.proxyPort=7890  
systemProp.https.proxyHost=127.0.0.1  
systemProp.https.proxyPort=7890  
# systemProp.file.encoding=UTF-8  
# org.gradle.warning.mode=all
```

**From: **https://developer.51cto.com/art/202006/619524.htm

## gradle.properties 文件：

gradle.properties:

```groovy
version=5.3.0-SNAPSHOT
## 设置此参数主要是编译下载包会占用大量的内存，可能会内存溢出
org.gradle.jvmargs=-Xmx2048M
## 开启 Gradle 缓存
org.gradle.caching=true
## 开启并行编译
org.gradle.parallel=true
## 启用新的孵化模式
org.gradle.configureondemand=true
## 开启守护进程 通过开启守护进程，下一次构建的时候，将会连接这个守护进程进行构建，而不是重新fork一个gradle构建进程
org.gradle.daemon=true
```

