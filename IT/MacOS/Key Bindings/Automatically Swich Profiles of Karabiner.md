# 使用 Keyboard Maestro 实现 Karabiner Elements 分应用自动切换 Profile：

## Karabiner 切换 Profile 的原理：

只要将`/Users/'whoami'/.config/karabiner/karabiner.json`文件中的 profiles 下的 name 的内容修改为对应的 Profile 名即可切换。

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

![Keyboard Maestros](/Users/fuck/Documents/Note/IT/MacOS/Keyboard Maestro.png)

From：https://invisprints.wordpress.com/2017/12/10/autochangekeyonmacos/

> 现在终于可以通过 Rime、karabiner Elements 和 Keyboard Maestro 来在任何情况下都使用 Emacs、终端快捷键了，自定义 YYDS。

相应的 Rime、Karabiner Elements 关键配置文件和 自动切换 Profile 脚本已经上传 GitHub 了。★