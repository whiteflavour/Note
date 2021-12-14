# 使用 Keyboard Maestro 实现 Karabiner Elements 分应用自动切换 Profile：

## Karabiner 切换 Profile 的原理：

只要将`/Users/'whoami'/.config/karabiner/karabiner.json`文件中的 profiles 下的 name 的内容修改为对应的 Profile 名即可切换。★

## 实现：

写一个自动切换的 PHP 脚本文件，配合 Keyboard Maestro 来实现自动切换：

### 脚本代码：

```php
#!/usr/local/bin/php
<?php
define('CONFIG_FILE', $_SERVER['HOME'].'/.config/karabiner/karabiner.json');
if (!file_exists(CONFIG_FILE)) {
    die('karabiner elements config file not found.');
}

$profileName = !empty($argv[1]) ? $argv[1] : 'Default profile';

$config = json_decode(file_get_contents(CONFIG_FILE), true);
$changed = false;
foreach ($config['profiles'] as $idx=>$profile) {
    if ($profile['name'] == $profileName) {
        $config['profiles'][$idx]['selected'] = true;
        $changed = true;
    } else {
        $config['profiles'][$idx]['selected'] = false;
    }
}

if ($changed) {
    file_put_contents(CONFIG_FILE, json_encode($config));
    system("/usr/bin/osascript -e 'display notification \"{$profileName}\" with title \"键盘布局\"'");
} else {
    die("Profile \"{$profileName}\" not found.");
}
```

From: https://github.com/xbot/shell/blob/master/karabiner-elements-profile-switcher.php

### Keyboard Maestro 创建宏：

切换 Profile 为 `Default`：

![Keyboard Maestros](/Users/fuck/Documents/Note/IT/MacOS/Key Bindings/Keyboard Maestro.png)

From：https://invisprints.wordpress.com/2017/12/10/autochangekeyonmacos/

> 现在终于可以通过 Rime、karabiner Elements 和 Keyboard Maestro 来在任何情况下都使用 Emacs、终端快捷键了，自定义 YYDS。

相应的 Rime、Karabiner Elements 关键配置文件和 自动切换 Profile 脚本已经上传 GitHub 了。★

## 更新 MacOS Monterey 后 KM 报错：“text-script：php：command not found” 问题解决：

### 原因：

KM 找不到 php 命令的路径：

更新 macOS Monterey 之后内置的 PHP 没了，所以要重新安装 PHP，其默认路径在`/usr/local/bin/php`；并且根据 Keyboard Maestro 的**官方文档*，KM 执行 Shell Script 的时候默认路径为`/usr/bin:/bin:/usr/sbin:/sbin`，没有重新安装 PHP 后的路径。

### 解决：

在 KM 中使用**绝对路径**执行 php 命令：`/usr/local/bin/php /Users/fuck/.config/karabiner/profile-switcher.php "Terminal"`。

### 感想：

更新系统后花了好几个小时都没解决：

1. 知识量不足，但前几天根据经验还是知道可能时路径问题，试过之后不行，没有把握，于是猜想可能是软件 Bug，但是据系统出来这么久，都还没修复，也不可能没人发现，所以暂时放弃了这个念头
2. 后来发现是单词拼写问题，switch 这个单词拼成了 swich，惹太多坑。。。

### 总结：

这个问题告诉我们：好好看**文档**总是没错的，有些问题在文档里就能知道答案。（印证了耗子叔的观点的正确性：先大致看看文档，掌握其脉络，后面遇到问题有个印象，方便查询答案。）★★

