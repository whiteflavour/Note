# 一些平时练习中遇到的问题 （Linux）

```bash
# 要加括号，否则只能列出大小为 0 的文件★
find /etc \( -type f -size +1500k -o -size 0 \) -exec ls -l {} \;
```

