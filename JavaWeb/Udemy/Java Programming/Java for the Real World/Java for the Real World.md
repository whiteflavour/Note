# Java for the Real World

## 1. The Java Virtual Machine (JVM)

### 1. JVM Overview

#### Java 代码的翻译：

Java 代码先被 JVM 翻译，然后再给操作系统。

**好处：**跨平台。★

#### Java Version：

##### 长期维护版本 (LTS —— Long Term Supported)：企业使用的版本 ★★

Java 8, 11, 14 ... 

#### JVM Varieties: 

Oracle 有两种 JDK ：Oracle JDK (相当于商业版 —— 收费) 和 Open JDK (免费) 。

区别：Oracle JDK 有一些特殊的功能，供大公司的特殊用途。★

> 除了 Oracle ，还有一些其他公司的 JDK ，才入门大可不必担心到底用哪个，那是后话。★

### 2. JVM Versions

#### 特点：

向下兼容。

> 注：如果在新版本上编译 Java 文件，然后在旧版本上运行，会报错；但是在旧版本上编译的则可以在新版本上运行。★

所以一定要保证你的电脑上的 Java 版本要跟服务器上的一致，否则就可能报上述错误，很尴尬。★★

## 2. Build Tools

### 3. Building Java Applications

> jar File 是跨平台的。

**存在 Build Tools 的原因：**

使用`javac`命令来构建 太麻烦了，而且也不好跨平台。★

### 4. Ant

**优点：**

灵活。

---

Ant 没有管理依赖 (dependencies management) 的工具，所以需要用到 Ivy ，它可以集成到 Ant 中。★

### 5. Maven

应用很广泛。

### 6. Maven: Navigating a POM File

