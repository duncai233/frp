基于[樱花内网穿透](https://github.com/ZeroDream-CN/SakuraPanel)改版而来
服务器使用[frpv0.60.0](https://github.com/fatedier/frp/releases/tag/v0.60.0)稳定版本

编译环境：Go 版本 go1.22.0 linux/amd64

功能和特性
支持多用户
支持用户组配置
支持为每个用户单独限速
支持为每个用户单独限制流量
支持配置签到获取流量
支持邀请码注册账号
实时流量统计
美观易用的界面
安装与配置
克隆项目至本地：

bash
复制
编辑
git clone https://github.com/walking-with-linght/sakurafrp
移动到网站目录并设置权限：

bash
复制
编辑
mv SakuraPanel/sakura/* /data/wwwroot/my.panel.com/
chown -R www:www /data/wwwroot/my.panel.com/
进入网站目录，编辑以下三个文件，修改数据库信息：

文件名	作用
/configuration.php	网站核心配置文件，包含详细注释
/api/index.php	用于对接 Frps，仅需配置 Token
/daemon.php	修改数据库信息，并设置为循环执行
使用 Navicat、phpMyAdmin 等数据库管理工具创建一个数据库，并导入 import.sql 文件。

数据库编码类型：utf8mb4 / utf8mb4_unicode_ci
数据库引擎：InnoDB
导入完成后，打开网站，注册一个新账号。接着，在数据库中将该账号的 group 字段设置为 admin，即可赋予管理员权限。

配套 Frps 服务端
为了兼容该面板，需要配置专用的 Frps 服务端。

Frps 必备配置：

toml
复制
编辑
bindPort = 7000  # frps 连接端口
auth.token = "abc"  # 连接 token，需与面板配置一致
webserver.addr = "0.0.0.0"  # 开启 web 管理
webserver.port = 7500  # 必须为 7500
webserver.user = "admin"  # 必须为 admin
webserver.password = "admin"  # 必须与节点配置一致
toml
复制
编辑
John_San_Api = "http://xxx.cn/api"  # 将 xxx.cn 替换为你自己的域名
john_san_token = "wobushitoken9527|1"  # 前半部分为 API Token，需与面板一致；后半部分为节点 ID
Frpc 客户端
Frpc 客户端无特殊要求，只需版本不高于 0.52 即可兼容使用。

