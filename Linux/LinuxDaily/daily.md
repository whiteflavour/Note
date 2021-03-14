# 一些平时练习中遇到的问题 （Linux）

```bash
# 要加括号，否则只能列出大小为 0 的文件★
find /etc \( -type f -size +1500k -o -size 0 \) -exec ls -l {} \;
```

---

## sudo 命令运行慢的问题：

原因：修改了计算机名（主机名）。

解决：`hostname`命令查看当前主机名，`vim /etc/hosts`，将返回的主机名（当前主机名）加入到 127.0.0.1 这一行中。

From：https://blog.csdn.net/xuwedo2003/article/details/4226933