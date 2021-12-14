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

> 注：更新 macOS Monterey 之后内置的 PHP 没了，所以要重新安装 PHP，其默认路径在`/usr/local/bin/php`；并且根据 Keyboard Maestro 的官方文档，KM 执行 Shell Script 的时候默认路径为`/usr/bin:/bin:/usr/sbin:/sbin`，没有重新安装 PHP 后的路径，所以在 KM 执行 php 命令时要使用**绝对路径**。（更新系统后花了好几个小时都没解决，还有个重大原因是单词拼写问题，switch 这个单词。。。）★★★

