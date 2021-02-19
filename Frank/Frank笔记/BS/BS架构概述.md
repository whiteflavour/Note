# B/S架构概述


[阅读数: 次   ](javascript:void(0);)[2020-03-14](https://wang_shuai_zhen.gitee.io/2020/03/14/BS架构概述/)

# 写在最前

> “考试的、学理论的给我滚！”
>
>  ——@Frank Xiang



# B/S学习笔记

## 1. 软件架构

**B/S 架构软件 —— 我们所有的东西都希望通过网站的形式使用，而不依赖于任何其他第三方环境，且依赖于浏览器的应用**

- B/S 通俗来说就是开发网站
  - Web程序 举例：office online
- C/S 架构 桌面应用 —— 基于C/C++的QT开发（岗位少）
  - WPS、office

## 2. 开发B/S架构软件需要哪些人才？

- 前端
- 后端
- 测试
- 运维 —— 管服务器、管部署
- 产品经理（PM）
- 首席技术官CTO【技术岗最高职位】（可能没有）
- 架构师【技术岗次高职位】

## 3. 前端准备

- VSCode
- Chrome/FireFox
- Node.js

设置淘宝镜像命令：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

**Yarn（可选）如果你要安装它，前提是必须安装Nodejs**

查看当前镜像源

```
config get registry
```

修改淘宝镜像

```
yarn config set registry https://registry.npm.taobao.org/
```

## 4. 前端预备课

### HTML

定义了网页内容的含义和结构

### CSS

网页的表现与展示效果

### JavaScript (JS)

功能与行为

### JS 框架

Jquery、Vue、React

### css 框架

bootstrap ELEUI

## 5. 后端预备课

### VMware 虚拟机

1.安全

2.与本机独立

3.可以把软件拖来拖去

4.快照——恢复到原来状态（速度还快）

```
# 备忘录——这台电脑用来学习的Ubuntu Server虚拟机

# ip
~$ ifconfig
# login
login as:qizong007
pswd:123456
```

### Linux基础 （类Unix：macOS）

#### 运维需要精通

Ubuntu 的问题搜索一定要带上版本号 （eg.16.04/18.04）

阿里镜像源

```
https://mirrors.aliyun.com/ubuntu/
```

拿到系统一定要先

```
sudo apt-get update
```

设置root密码

```
sudo passwd root
```

小火车试运行：sl

```
ctrl+L # 清屏
ctrl+U # 清行
ls -a # 查看隐藏文件
```

安装必要软件

```
sudo apt-get install openssh-server
```

#### ssh连接

本质——传输命令

```
ssh id@xxx.xxx.x.x(IP)
```

公司不会给你暴露IP地址，但会给你密钥，你离职时会删除

推荐：XShell 功能更强，但是要钱；我们用的是PuTTY

#### 代码怎么放到网站上？

文件传输 基于FTP协议

1.部署到GitHub等代码管理上（如Git）【现在都用这个】

2.FTP传输

查看IP

```
~$ ifconfig
```

查看内存（-m 以MB为单位 ~代表用户目录）

```
~$ free -m
```

补全命令

```
tab键
```

进入工程文件夹

```
vim .
```

#### yarn是个啥

**“安全+可靠+快”的包管理器（基于npm)**

**注意yarn的安装:**

第一步——配置仓库

```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

第二步——安装

```
sudo apt-get update && sudo apt-get install yarn
```

第三步——确认安装

```
yarn -v
```

配置

```
yarn config set registry https://registry.yarnpkg.com
```

安装pm2

```
yarn global add pm2
```

### 后端语言：Java/Go/Node.js/C#(.NET)/Python/PHP

> JSP -> html 里面扩展java代码 eg: <%for…%>
>
> 不利于业务拓展

- 现在已经前后端分离

### HTTP服务器搭建软件：Tomcat/Nginx/Apache

- 比如Tomcat，给某个IP开放一个端口（8080）
- 下面两者都是3000！

#### Express (Node.js的框架)的搭建

- 轻量级web开发框架

```
~$ yarn init
~$ git init
~$ yarn add express # 安装
~$ touch app.js # 复制helloworld代码
~$ node app.js # 启动服务
# 在app.js中app.get()上添加：
app.use(express.static('public'));
~$ mkdir public
~$ cd public
~$ vim hello.html # 随便写个静态网页
~$ cd ..
~$ node app.js # 启动服务，进入/public，就看的到了
```

#### pm2

**pm2是一个进程管理工具,可以用它来管理你的node进程，并查看node进程的状态，当然也支持性能监控，进程守护，负载均衡等功能**

```
~$ sudo yarn global add pm2
# 进入目标工程文件夹下
~$ pm2 start app.js # 启动服务，可以在同个工程下页面间互相链接了
```

- 区别
  - node app.js 只是短暂开启服务，而且没有优化
  - pm2 start app.js 只要服务器不关，就一直开着，还有优化

### MVC模式

model 模型

service 层

controller 控制器

### HTTP API

### 数据库：MySQL/Oracle/SQL Server/SQLite/MongoDB/Redis

- 背景：因为我们前面搭的都是**静态页面**——**无数据交互**！
- **动态页面** ：和用户之间具有数据交互
- 将数据存到txt中，纯属扯淡！！！
- 存到excel中，稍好一点…至少有“**表**”了！但是过于庞大…
- 更好的就是数据库！它本身也是有单独数据类型的，小数计算没有偏差，本质也是个文件。一个库相当于好多个excel表。
- 初学者就是CRUD，对数据的增删改查
- 学牛了，在考虑优化
- 初学者学一个T-SQL和一个NO-SQL：**MySQL和Redis**
- 版本推荐：MySQL 5.7
- 下载链接：https://dev.mysql.com/downloads/mysql/5.7.html
- Linux下安装配置：https://blog.csdn.net/weixx3/article/details/80782479
- 安装时点**开发者默认即可**
- 切记！**用后端语言去驱动！**
- 推荐图形化界面：Navicat
- 推荐框架：ORM（@注释搞定，不用写sql语句，疯狂用API）

## 6. Git（前端后端——必学，很重要！）

开发人员：Linux作者（用C写的）

1. 版本控制 保留了一切的历史 可以让代码迅速恢复到你想指定的commit位置

 1 2 3（比如3有bug，回滚回2）【时光穿梭】

1. 协作开发 —— 需要网络

在自己的电脑上使用git，那确实是有版本控制功能，没有协作开发功能

大家把每次写的东西放到哪？ 基于Git的一个平台—— GitHub，GitLab，码云

1. 如何放在Linux上部署运行？网站是怎么运行的？

   过程：各自开发，git push上传——测试成功，git合并——架构师那跑成了，git pull更新

## 7. 全栈

- 前端 -> 后端 比较多 -> node.js

## 8. Devops

- 开发+质量检测+技术运营

## 9. github

- 克隆（尽量别直接Download）

```shell
~$ git clone url
```