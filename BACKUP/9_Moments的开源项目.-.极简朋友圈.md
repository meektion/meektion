# [Moments的开源项目 - 极简朋友圈](https://github.com/meektion/meektion.github.io/issues/9)

# Moments - 极简朋友圈

[![release](https://img.shields.io/badge/release-更新记录-blue)](https://github.com/kingwrcy/moments/releases)
[![docker-release-status](https://img.shields.io/github/actions/workflow/status/kingwrcy/moments/docker-image-release.yml)](https://github.com/kingwrcy/moments/actions/workflows/docker-image-release.yml)
[![docker-pull](https://img.shields.io/docker/pulls/kingwrcy/moments)](https://hub.docker.com/repository/docker/kingwrcy/moments)
[![telegram-group](https://img.shields.io/badge/Telegram-group-blue)](https://t.me/simple_moments)
[![discussion](https://img.shields.io/badge/moments-论坛-blue)](https://discussion.mblog.club)

从 v0.2.1 开始，使用 Golang 重写了服务端, 目前已经基本实现了 0.2.0 版本的功能，同时软件包体积也更小了。

注意：如果你在找 v0.2.0 版本，请 [点击这里](https://github.com/kingwrcy/moments/blob/master/README.md)。

# 功能列表

- 默认用户名和密码是 admin/a123456，登录后可以在后台修改
- 多用户模式，后台可以自由开启是否运行注册多用户
- 标签的定义，以 # 号开头，空格 / 空行结尾的中间的部分会被认为是标签
- 在 memo 发言的输入框里点击右键可以选择标签来插入
- 支持完整的 Markdown，但是目前样式只适配了常用的几个标签，更多的待接下来完善
- 代码块支持一键复制按钮
- 支持回到顶部按钮，PC 端和手机端都有

更多说明可以[点击这里查看](https://discussion.mblog.club/post/pto2hqoFzDKzZMpvoPZKYuP)。

# 使用教程

## 环境变量

Moments 支持以下环境变量，可按需修改进行配置：

| 变量名            | 解释                  | 默认值                                                 |
| ----------------- | --------------------- | ------------------------------------------------------ |
| PORT              | 监听端口              | 3000                                                   |
| JWT_KEY           | JWT 密钥              | 不填写则每次启动时随机生成，每次重启后需要重新登录     |
| DB                | sqlite 数据库存放目录 | 工作目录下的 db.sqlite，/app/data/db.sqlite            |
| UPLOAD_DIR        | 上传文件本地目录      | 工作目录下的 upload，/app/data/upload                  |
| LOG_LEVEL         | 日志级别              | info，可选 debug                                       |
| ENABLE_SWAGGER    | 是否启用 swagger 文档 | false，可选 true，启用后可访问路径 /swagger/index.html |
| ENABLE_SQL_OUTPUT | 是否启用 SQL 调试日志 | false                                                  |

## 使用 Docker

注意：需要将以下示例中的 $JWT_KEY 替换为你的真实 JWT_KEY，生成方式可[参考这里](#jwt_key-生成)。

使用命令行启动容器：

```bash
docker run -d \
  -e PORT=3000 \
  -e JWT_KEY=$JWT_KEY \
  -p 3000:3000 \
  -v /var/moments:/app/data \
  --name moments \
  kingwrcy/moments:latest
```

也可以使用 Docker Compose:

```yaml
services:
  moments:
    image: kingwrcy/moments:latest
    container_name: moments
    restart: always
    environment:
      PORT: 3000
      JWT_KEY: $JWT_KEY
    ports:
      - 3000:3000
    volumes:
      - /var/moments:/app/data
```

## 使用二进制文件

待补充

## JWT_KEY 生成

### 使用 OpenSSL

执行以下命令生成 (仅测试了 Linux)：

```bash
openssl rand -hex 32
```

### 使用 SHA256

执行以下命令生成 (仅测试了 Linux)：

```bash
echo $RANDOM | sha256sum
```

### 在线生成

打开 [https://tool.lu/uuid](https://tool.lu/uuid) 生成不带 `-` 的 UUID 作为 JWT_KEY。

# 其他版本

| 项目                                                            | 演示地址                                                             |
| --------------------------------------------------------------- | -------------------------------------------------------------------- |
| [RandallAnjie/moments](https://github.com/RandallAnjie/moments) | [https://moments.randallanjie.com](https://moments.randallanjie.com) |

