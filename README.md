# 基于 [樱花内网穿透](https://github.com/ZeroDream-CN/SakuraPanel) 改版而来

服务器使用 [frpv0.60.0](https://github.com/fatedier/frp/releases/tag/v0.60.0) 稳定版本

编译环境：**go version go1.22.0 linux/amd64**

---

## 功能和特性

- 支持多用户
- 支持用户组配置
- 支持每个用户单独限速
- 支持每个用户单独限制流量
- 可配置签到获得流量
- 可配置凭邀请码注册账号
- 实时流量统计
- 美观的界面

---

## 安装和配置

1. **克隆项目到本地**

   ```bash
   git clone https://github.com/walking-with-linght/sakurafrp
    ```
2. **移动到网站目录，并设置权限**

  ```bash
    mv SakuraPanel/sakura/* /data/wwwroot/my.panel.com/
    chown -R www:www /data/wwwroot/my.panel.com/
```

3. **编辑配置文件**

进入网站目录后，分别编辑以下三个文件，修改数据库信息：

| 文件名              | 作用说明                                  |
|--------------------|---------------------------------------|
| configuration.php  | 网站核心配置文件，里面每个配置项都有介绍      |
| api/index.php      | 用于对接 Frps，里面只需配置 Token            |
| daemon.php      | 需要修改数据库信息，需要设置循环执行    |

5. **创建数据库并导入数据**

   - 使用 Navicat、phpMyAdmin 等数据库管理软件创建一个数据库。
   - 设置数据库的 **编码类型** 为 `utf8mb4`，**排序规则** 为 `utf8mb4_unicode_ci`。
   - 设置数据库的 **引擎** 为 `InnoDB`。
   - 导入 `import.sql` 文件到数据库中。

   
6. **注册与管理员设置**

   - 导入完成后，打开网站，注册一个新账号。
   - 在数据库中，找到该账号的记录。
   - 将该账号的 `group` 字段设置为 `admin`，即可将该账号设置为管理员。










