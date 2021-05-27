# Linux课程：初级到高级用户 （Ubuntu）

## Linux 小知识 （Ubuntu）

在资源管理器中按 Ctrl + h 显示隐藏文件。

终端中 ^ 表示的是 Ctrl 键。

super 键为 Win 键。

## Linux 发行说明

许多 Linux 发行版都是基于 Debian 框架。（包括 Ubuntu ）

**Linxu kernal 的作用**：联系硬件与软件。

## 禁用ISO和第一开机

取消勾选使用安装时的镜像文件。

## 定制 Ubuntu 桌面

gnome-look.org

## 统一调整工具

Unity Tweak Tool

## 装双系统

1. 浏览器搜索 unetbootin.sourceforge.net
2. 点击 Download(Windows)
3. 格式化 U 盘（至少8GB）
4. 电源设置中关掉快速启动选项
5. 重启进入BIOS
6. 选择 USB 启动

## Linux 命令行

### 基础部分：

`-` 叫做 dash 。

~ ：相当于 /home/username

/  (forward slash)：后面跟绝对目录

./ ：后面跟相对目录

../ ：返回上一级

`&&`：在两条命令之间使用，第一条执行完成之后执行第二条。

---

clear ：清空终端上已执行过的命令

`ls --help` ：帮助

sudo ：superuser do，获得编辑文件的权限。

!! ：执行上一条命令

### 关于切换到 root 权限：

sudo su ：获得 root 权限（使用 root 用户）

su username ：返回自己的用户

### nano 编辑文件：

nano ./file ：查看文件

sudo nano ./file ：若文件存在，则编辑它；若文件不存在，则创建并编辑它。

sudo nano file.txt：创建并编辑一个名为 file.txt 的文件

---

### apt-get，apt-cache 安装软件：

sudo apt-get install xxx ：从仓库下载应用

sudo apt-get remove xxx ：卸载应用

apt-cache search xxx ：从仓库中搜索有关应用

apt-cache policy xxx ：查看应用的信息

**下载仓库中没有的应用**：从浏览器中下载安装包，进入安装包目录，使用命令 `sudo dpkg -i ./安装包名`，然后在命令行中运行

sudo apt-get upgrade ：更新库中的应用

---

### 关于 ls -l ：

![命令 ls -l 下的一些说明](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\命令 ls -l 下的一些说明.png)

r 表示 readable ，w 表示 writable ，x 表示 executable 。

---

**修改权限**：

sudo chown root:fuck（user:group） file.txt ：修改该文件的拥有者

sudo chmod 664 file.txt ：修改该文件的权限，6 表示该文件能够读写，4表示只读，7表示目录（一般不使用）

sudo chown -R nick:nick ./mydir ：将该目录及它里面的文件全部修改所有权。 -R 表示 recursive 。

### 关于文件管理（创建、删除、拷贝、移动）：

rm file.txt ：删除文件

touch file.txt file2.txt file3.cpp file4.txt ：创建若干文件

rm ./mydir/*.cpp ：删除该目录中所有的 cpp 文件

rm -rf ./mydir ：删除该目录

cp file ./mydir/file2 ：拷贝该文件

mv filename filename2 ：移动该文件，可用来重命名文件（目录）

---

### find 查找：

find . -type f -name " *.php " ：在当前目录下，查找所有的 php 文件，不忽略大小写。f 表示文件，d 表示目录。

find . -type f -iname " *.php " ：在当前目录下，查找所有的 php 文件，忽略大小写。

find . -type f -perm 0664 ：根据权限查找

find . -size +1M ：根据文件大小查找，查找1M以上的文件。- 代表以下，不加符号代表确切的大小。

find . -type f -not -iname " *.php " ：查找不是 php 的文件

find . -maxdepth 1 -type f -iname " *.conf " ：maxdepth 表示最多只寻找一个目录 ( -maxdepth 只能在 -type 的前面，否则报错)

![find 注意事项](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\find 注意事项.png)

---

### grep 查找文本：

grep "function" file.php ：在 file.php 文件中查找 function

grep "function" file.php file2.php ：在这两个文件中查找 function

grep -i "function" ./* ：忽略大小写，在该目录中查找function

grep -n -i "function" ./* ：-n 表示显示 function 的行号

### find 与 grep 配合查找：

find . -type f -iname "*.php" -exec grep -i -n "function" {} + ：-exec 表示 execute ，{} + 表示 -exec 的结束标志。 

find . -type f -size -10k -iname "*.php"  -exec grep -i -n "function" {} + ：find 查找两个参数

ls > outfile.txt ：将该命令的结果输出到该文件中

find . -type f -size -10k -iname "*.php" -exec grep -i -n "sandwich" {} + > f.txt ：结合 find ，grep 输出

find . -type f -size -10k -iname "*.php" -exec grep -i -n "function" {} + | tee of.txt ：将结果输出到 of.txt 文件中，<u>并且输出到屏幕上</u>

---

### top 查看进程：

top ：Linux 上的任务管理器，查看任务进程。Ctrl + C 退出。

![top 命令](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\top 命令.png)

PID ：process ID ，USER ：该应用的创建者，TIME+ ：该应用已运行的时间，COMMAND ：与该进程相关的命令。

---

ps aux ：更完整的任务管理器。

ps aux | grep liri-browser ：搜索所有有关 liri-browser 的进程。

pgrep liri-browser ：搜索所有正在运行的 liri-browser 这个应用的 PID 。（从上到下按顺序排列，最上面的是最先打开的那个对应的 PID）

kill -9 6300 ：杀死 PID 为 6300 的那个进程。

kill -9 6186 6358 ：杀死 PID 为 6186 和 6358 的这两个进程。

killall liri-browser ：杀死所有的 liri-browser 进程

---

### Services：

**古老的方式管理服务**：*uses services*：（不推荐使用）

sudo service elasticsearch start ：开启 elasticsearch 服务 （可以在浏览器中输入 localhost:9200 查看）

sudo service elasticsearch stop ：停止 elasticsearch 服务 （此时已经无法进入 localhost:9200）

**修改 localhost 端口号**：

1. sudo service elasticsearch start （开启服务）

2. find /etc -type f -iname "elasticsearch*" （查找 yml 文件）

3. sudo nano /etc/elasticsearch/elasticsearch.yml （修改配置文件）

4. 将文件中的端口号改为 1150 ，保存，退出。（但是现在还未生效，需重启服务）

    ![修改端口号](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\修改端口号.png)

---

5. sudo service elasticsearch restart  （重启服务）（现在服务已生效）

**现代方式管理服务**：*uses systemctl*：（推荐使用的方式）

sudo systemctl start elasticsearch ：开启 elasticsearch 服务 （等价于 sudo service elasticsearch start）

sudo systemctl stop elasticsearch ：停止 elasticsearch 服务 （等价于 sudo service elasticsearch stop）

*这两者唯一的不同在于 `start` 和 `stop` 在命令中出现的位置！*

---

### 使用 crontab 来定时执行命令：

crontab -e ：进入文本，找到最后一行，可以进行修改，自行添加命令：

![关于 crontab -e](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\关于 crontab -e.png)

![crontab 定时执行任务的命令的格式](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\crontab 定时执行任务的命令的格式.png)

最后一行为要定时执行的命令。

sudo crontab -e ：以管理员的身份运行。（可以用来定时更新软件）

### 安装 IDE

#### 安装 jdk：

sudo apt-get install openjdk-8-jre ：安装 jdk 8

sudo apt-get install openjdk-9-jre ：安装 jdk 9

PyCharm 如果要创建桌面快捷方式，需要保证 pycharm.sh 文件允许被执行。★

## Git

### 安装 Git ：

sudo apt-get install git git-extras ：安装 Git

### 使用 Git ：

### 创建分支并与远程仓库中的分支关联：

1. 选择一个目录，创建一个项目，在其中创建源文件，例如 main.py 、main.cpp ......
2. `git init` ：在此目录下初始化仓库。
3. 进入 Github ，创建一个仓库。
4. 复制仓库链接 (HTTP) 。
5. 终端输入命令 ：`git remote add origin 刚刚复制的地址` 。
6. 配置用户名：`git config --global user.name "Nick"`。（第一次使用 git 时使用）
7. 配置邮箱：`git config --global user.email 1311798851@qq.com`。（第一次使用 git 时使用）
8. `git pull origin master` ：从分支中获取并集成。
9. 终端输入 `ls` 命令，会发现该目录下多了一个 README.md 文件。
10. `git branch --set-upstream-to=origin/master` ：将本地分支与远程分支 master 关联。

### 修改分支中的文件并将其发送给服务器：

1. 打开 IDE ，发现项目中多了一个 README.md 文件。

2. 在 IDE 中修改文件。

3. `git add README.md` ：将修改的文件（这里是 README.md）添加到追踪器。

    `git add -A` ：将所有修改的文件添加到追踪器。

4. `git commit -m "Updated readme, added main.py"`：提交修改，并在 `""`中注释对修改的一些描述，但不能太长，因为是要显示到 github 上的，太长了不太方便。

5. 如果没有将 upstream 设置为 origin master ，那么使用：`git push origin master`；如果前面设置了，使用：`git push` ，并输入用户名和密码。

6. 刷新 github 的页面。

### 删除 github 中的文件并提交：

1. `git rm -r .idea` ：删除 .idea 目录。
2. `git add -A` 或者 `git add .idea` ：将修改添加到 tracker 。
3. `git push` ，并输入用户名和密码 ：提交服务器。
4. 刷新 github 页面。

### 再次删除 .idea 文件：

1. `git rm -r -f .idea` ：加上 `-f` 的原因是 .idea 文件已经被修改过了。
2. `git add -A` 。
3. `git commit -m "Remove .idea directory for real"` 。
4. `git push` 。
5. 刷新 github 页面。

### 忽略 .idea 目录：（每次打开 Jetbrains 的 IDE 时都会自动创建一个 .idea 文件，如果不想让它在仓库中出现，则可以忽略它）

`sudo nano ./.gitignore`：创建 .gitignore 文件，将要忽略的文件写入其中，即可忽略。

---

### 在终端上解决 merge conflict

**构造 merge conflict**：

1. 创建一个新的目录，在新目录上添加初始化 git ，添加远程源并 `pull` 。
2. 修改目录中的文件，添加、提交并 `push` 。
3. 返回原来进行过 git 操作的目录，修改该目录中的文件，当执行 `push` 操作时，会提示错误。
4. 输入命令：`git fetch origin master`。
5. 输入命令：`git merge / pull`，会提示 merge conflict 。
6. 用 gedit / nano 打开该目录下刚刚修改的那个文件，会提示该文件在硬盘中已经修改，点击 reload ，会发现文件多了许多奇怪的符号：

![Git Merge Conflict](F:\笔记\YouTube\Linux\Linux基础\Joseph Delgadillo\Git Merge Conflict.png)

7. 将那些符号删去，保存，输入命令：`git add -A` ，`git commit -m "merge conflicts resolved"`，`git push`。
8. 刷新 github ，会发现文件已经修改成功。

### 设置和管理分支：

可以在 IDE 中快速 push，commit ，创建分支等等。

**创建分支**：`git branch xxx`

创建完成之后在此目录中修改文件，然后 add, commit, push ，刷新 github 页面，会发现多了一个分支。

**创建分支的好处**：如果一个团队共同开发一个项目，那么可以每人使用一个分支，这样 push 的时候就不会互相干扰。

**将另一个分支中的文件 push 到 master 中**：

1. `git checkout master`：将分支切换到 master
2. `git merge b2 master`：将分支 b2 融合到 master
3. `git push origin master`：push 分支master
4. 刷新 github 页面，就会发现已经将刚刚在另一个分中更新的修改的文件 push 到了 master 中

### Git 的优点：

适合开发大型项目，一个团队共同开发。

## Meteor：Build JS Application

### Meteor 的安装与初步使用：

**安装 Meteor**：在官网上去复制命令，需要先安装 curl。

**创建项目**：`meteor create todo`：创建一个名为 todo 的项目

**运行程序**：在项目的目录下使用命令 `meteor` ，运行该项目。

**将包添加到项目中**：`meteor add twbs:bootstrap`：添加 twbs:bootstrap 包。（可以去 Atmosphere 中寻找 package。）

























