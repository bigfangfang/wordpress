###安装好数字证书，一开始chrom 提示是一个小锁🔒，但是点到其他页面又提示不安全，虽然是https://ilileyou.gq 但是还是有不安全的提醒。是怎么回事呐？
我们要到 SSH界面下（黑色的界面）

输入第一句 编辑worpress 配置文件
sudo vi /opt/bitnami/apps/wordpress/htdocs/wp-config.php

键盘输入 i 可编辑状态
键盘上下左右 找到

找到
define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST'] . '/');
define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST'] . '/');
替换成
define('WP_SITEURL', 'https://' . $_SERVER['HTTP_HOST'] . '/');
define('WP_HOME', 'https://' . $_SERVER['HTTP_HOST'] . '/');

第二句：
sudo /opt/bitnami/ctlscript.sh restart
