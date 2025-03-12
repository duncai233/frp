<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>樱花内网穿透改版配置</title>
</head>
<body>
    <h1>基于 <a href="https://github.com/ZeroDream-CN/SakuraPanel">樱花内网穿透</a> 的改进版</h1>
    <p>服务器使用 <a href="https://github.com/fatedier/frp/releases/tag/v0.60.0">frp v0.60.0</a> 稳定版本</p>
    <p>编译环境：<strong>Go 版本 go1.22.0 linux/amd64</strong></p>

    <h2>功能和特性</h2>
    <ul>
        <li>支持多用户</li>
        <li>支持用户组配置</li>
        <li>支持为每个用户单独限速</li>
        <li>支持为每个用户单独限制流量</li>
        <li>支持配置签到获取流量</li>
        <li>支持邀请码注册账号</li>
        <li>实时流量统计</li>
        <li>美观易用的界面</li>
    </ul>

    <h2>安装与配置</h2>
    <h3>1. 克隆项目至本地</h3>
    <pre><code>git clone https://github.com/walking-with-linght/sakurafrp</code></pre>

    <h3>2. 移动到网站目录并设置权限</h3>
    <pre><code>mv SakuraPanel/sakura/* /data/wwwroot/my.panel.com/
chown -R www:www /data/wwwroot/my.panel.com/</code></pre>

    <h3>3. 进入网站目录，编辑以下三个文件，修改数据库信息</h3>
    <ul>
        <li><code>/configuration.php</code> - 网站核心配置文件，包含详细注释</li>
        <li><code>/api/index.php</code> - 用于对接 Frps，只需配置 Token</li>
        <li><code>/daemon.php</code> - 修改数据库信息，并设置为循环执行</li>
    </ul>

    <h3>4. 使用 Navicat 或 phpMyAdmin 等数据库管理工具创建数据库，并导入 import.sql</h3>
    <p>数据库编码类型：<code>utf8mb4 / utf8mb4_unicode_ci</code></p>
    <p>数据库引擎：<code>InnoDB</code></p>

    <h3>5. 导入完成后，打开网站，注册新账号</h3>
    <p>在数据库中将账号的 <code>group</code> 字段设置为 <code>admin</code>，赋予管理员权限</p>

    <h2>配套 Frps 服务端</h2>
    <pre><code>
# Frps 必备配置
bindPort = 7000                # frps 连接端口
auth.token = "abc"             # 连接 token，需与面板配置一致
webserver.addr = "0.0.0.0"     # 开启 web 管理
webserver.port = 7500          # 必须为 7500
webserver.user = "admin"       # 必须为 admin
webserver.password = "admin"   # 必须与节点配置一致
    </code></pre>

    <pre><code>
John_San_Api = "http://xxx.cn/api"  # 将 xxx.cn 替换为你自己的域名
john_san_token = "wobushitoken9527|1"  # 前半部分为 API Token，需与面板一致；后半部分为节点 ID
    </code></pre>

    <h2>Frpc 客户端</h2>
    <p>Frpc 客户端无特殊要求，只需版本不高于 <code>0.52</code> 即可兼容使用。</p>
</body>
</html>
