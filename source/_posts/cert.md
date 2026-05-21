---
title: Let's Encrypt证书申请方法汇总
date: 2025-05-17 12:59:07
tags: 持续更新
categories: 探索
---

申请SSL证书是搭建网站过程中必不可少的一环，下面汇总了一些申请Let's Encrypt证书的方法。

为什么要选择Let's Encrypt证书？因为它通用性强而且免费啊！

<!-- more -->

注：下面这些方法是我用chatgpt得到的方案，个人认为还是相对来说比较清晰且简单的。全文都以为我的网站申请SSL证书为例。

------

# 方法一：用 acme.sh 申请通配符证书（阿里云 DNS 验证）

### 1. 安装 acme.sh

```bash
curl https://get.acme.sh | sh
# 安装后，需要执行下面命令让 acme.sh 命令生效：
source ~/.bashrc
```

------

### 2. 配置阿里云 API 凭证（DNS-API 验证必需）

你需要去阿里云控制台：

- 进入「RAM 控制台」-> 创建一个 AccessKey（含访问阿里云 DNS 的权限）
- 拿到 `AccessKey ID` 和 `AccessKey Secret`

然后在服务器执行：

```bash
export Ali_Key="你的AccessKey ID"
export Ali_Secret="你的AccessKey Secret"
```

为了每次都生效，可以把这两行写到 `~/.bashrc` 或 `~/.profile` 里。

------

### 3. 申请证书（包括根域和通配符）

```bash
acme.sh --issue --dns dns_ali -d guyue.me -d '*.guyue.me'
```

- `--dns dns_ali` 表示用阿里云 DNS API 做验证
- `-d guyue.me` 是根域证书（因为通配符证书本身不包含根域）
- `-d '*.guyue.me'` 是通配符证书

------

### 4. 安装证书并设置自动续期及重载 Nginx

```bash
acme.sh --install-cert -d '*.guyue.me' \
--key-file /etc/ssl/guyue.me/private.key \
--fullchain-file /etc/ssl/guyue.me/fullchain.cer \
--reloadcmd "systemctl reload nginx"
```

- 这里会把私钥和证书安装到指定路径
- 并在续期后自动执行 `systemctl reload nginx` 让证书即时生效

------

### 5. 配置 Nginx（示例）

```nginx
server {
    listen 443 ssl;
    server_name guyue.me *.guyue.me;

    ssl_certificate /etc/ssl/guyue.me/fullchain.cer;
    ssl_certificate_key /etc/ssl/guyue.me/private.key;

    # 其他 SSL 参数略
}
```

------

### 6. 验证续期状态

你可以运行：

```bash
acme.sh --cron
```

它会检查并自动续期（默认每24小时运行一次）。

建议配置定时任务（cron）：

```bash
crontab -l
# 如果没有，可以用下面命令添加（每天凌晨1点执行续期）
echo "0 1 * * * \"$HOME/.acme.sh\" --cron --home \"$HOME/.acme.sh\" > /dev/null" | crontab -
```

------

### 总结

- 你现在能完全自动申请和续期证书，无需每 90 天手动操作
- 证书安全地存储在你服务器里，自动给 Nginx 更新
- 适合长期稳定运行

------





# 方法二：用 ohttps.com 申请 SSL（通配符）证书流程

### 1. 注册登录

- 访问 [ohttps.com](https://ohttps.com/)
- 注册账号并登录

------

### 2. 添加域名

- 在后台点击“添加域名”或“新建证书”
- 填写你的主域名，比如 `guyue.me`
- 选择申请 **通配符证书**，一般是 `*.guyue.me`

------

### 3. 选择验证方式

ohttps.com 支持多种验证：

- **DNS 验证（推荐通配符证书）**
  - 系统会给你一个 TXT 记录的值
  - 你需要去你的域名 DNS 服务商（比如阿里云控制台）添加对应的 TXT 记录
- **HTTP 验证**
  - 需要你在网站根目录放置特定文件验证（通配符证书一般不支持）

------

### 4. 添加 DNS TXT 记录

- 登录你的域名 DNS 控制面板
- 添加 ohttps.com 提供的 TXT 记录内容
- 等待 DNS 解析生效（一般几分钟到几十分钟不等）

------

### 5. 触发验证并颁发证书

- 回到 ohttps.com 后台，点击“验证”或者“申请”
- 系统自动验证 DNS 记录
- 验证成功后，证书颁发成功

------

### 6. 下载证书文件

- 证书颁发后，ohttps.com 提供下载
- 通常包括：
  - **证书文件**（.crt 或 .cer）
  - **私钥文件**（.key）
  - 可能还有中间证书或全链证书

------

### 7. 上传证书到服务器

- 把证书和私钥文件上传到服务器指定目录（如 `/etc/ssl/guyue.me/`）
- 配置 Nginx 或 Apache 使用这些证书文件

------

### 8. 配置服务器

以 Nginx 为例，修改配置：

```nginx
ssl_certificate /etc/ssl/guyue.me/fullchain.cer;
ssl_certificate_key /etc/ssl/guyue.me/private.key;
```

然后重载 Nginx：

```bash
sudo systemctl reload nginx
```

------

### 9. 续期管理

- ohttps.com 的证书有效期一般是 90 天
- 到期前需重新在 ohttps.com 申请并重复上传
- 你可以设置提醒避免过期

------

### 总结

| 优点               | 缺点               |
| ------------------ | ------------------ |
| 简单易用，界面友好 | 续期需手动操作     |
| 支持通配符证书     | 无自动续期脚本     |
| 无需安装客户端工具 | DNS 记录需手动添加 |

