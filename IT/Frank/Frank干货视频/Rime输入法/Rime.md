# Rime

## Rime 输入法的安装

1. 安装时自己指定一个目录进行安装
2. 安装过程中会弹出一个安装选项的方框，第二栏：用户资料夹，选择我来指定位置，建议放在第一步的安装目录下，并创建一个新目录 MyConfigData 。例如：D:\Software\Rime\MyConfigData 。![Rime安装选项](F:\Note\Frank\Frank干货视频\Rime输入法\Rime安装选项.png)

3. 安装完成后将微软自带的输入发删掉

## 设置

按 F4 可以选择输入的语言。

在右下角任务栏右击 Rime 输入法的图标，点击输入法设定，只留下简化字。

## 补丁配置包

### 将输入格式变为横向：

1. 解压补丁配置包，将 default.custom.yaml 与 weasel.custom.yaml 文件复制到 \MyConfigData 目录中，覆盖同名文件
2. 重新部署一下

为什么这样做后会变成横向的？可以打开 weasel.custom.yaml 这个配置文件看看。

而输入框中有 9 个字，跟 default.custom.yaml 这个配置文件有关。

那个 build 目录中是一些与刚刚右键打开的输入法设定相关的一些内容。

## 添加字符输入：

1. 将补丁配置包中的 luna_pinyin_simp.custom.yaml 文件拷贝到 \MyConfigData 目录中
2. 重新部署

该输入的说明在 D:\Rime\Rime\weasel-0.14.3\data\symbols.yaml 文件中。★

### 添加英文输入法：

1. 解压
2. 将里面的两个文件依旧复制到 \MyConfigData 中
3. 重新部署
4. 按 F4 选择 Easy English
5. 输入英文

easy_en.dict.yaml 文件为英文词库。★

---

后台有个小狼毫的服务，自动计算你打某字的频率。

Mac 用户可以将输入法改成圆角，可以网上去搜，自己配。★





































