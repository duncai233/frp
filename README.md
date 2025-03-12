

基于[樱花内网穿透](https://github.com/ZeroDream-CN/SakuraPanel)改版而来

服务器使用[frpv0.60.0](https://github.com/fatedier/frp/releases/tag/v0.60.0)稳定版本


基于**go version go1.22.0 linux/amd64**编译

功能和特性
支持多用户
支持用户组配置
支持每个用户单独限速
支持每个用户单独限制流量
可配置签到获得流量
可配置凭邀请码注册账号
实时流量统计
美观的界面

安装和配置
首先将项目 clone 到本地

git clone https://github.com/walking-with-linght/sakurafrp
接着移动到网站目录，并设置权限

mv SakuraPanel/sakura/* /data/wwwroot/my.panel.com/
chown -R www:www /data/wwwroot/my.panel.com/
然后进入到网站目录，分别编辑以下三个文件，修改数据库信息

文件名	作用
/configuration.php	网站核心配置文件，里面每个配置项都有介绍
/api/index.php	用于对接 Frps，里面只需配置 Token
/daemon.php	需要改数据库信息 需要设置循环执行
配置完成后，使用 Navicat、phpMyAdmin 等数据库管理软件创建一个数据库，然后导入 import.sql。

数据库编码类型：utf8mb4 / utf8mb4_unicode_ci；数据库引擎：InnoDB

导入完成后，打开网站，注册一个新账号，然后在数据库中设置这个账号的 group 字段为 admin 即可设置为管理员。

配套 Frps 服务端
本面板需要专用 Frps 才能兼容

frps必备配置
bindPort = 7000 //frps连接端口
auth.token = "abc" //连接token需要和面板一样
ebserver.addr = "0.0.0.0" //需要开启web管理
webserver.port = 7500  //必须要7500
webserver.user = "admin" //必须要admin
webserver.password = "admin" //和节点设置里一样

John_San_Api = "http://xxx.cn/api" //xxx.cn换成你自己的域名
john_san_token = "wobushitoken9527|1" //前面是api Token 需要和面板一致 后面是节点id

Frpc 客户端无特殊需求，只要版本是 =>0.52 都可以兼容使用。
