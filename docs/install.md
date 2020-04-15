# 部署

## Docker 部署

### 1. 下载配置文件
在项目目录下新建 `config.yml` 文件


```bash
mkdir ~/flowerss123 &&\
wget -O ~/flowerss123/config.yml \
    https://raw.githubusercontent.com/indes/flowerss-bot/master/config.yml.sample
```


### 2. 修改配置文件

```bash
vim ~/flowerss/config.yml
```

### 3. 运行

```shell script
docker run -d -v ~/flowerss:/root/.flowerss indes/flowerss-bot
```

## 二进制部署

从 [Releases](https://github.com/indes/flowerss-bot/releases) 页面下载对应的版本。

## 源码编译部署

```shell script
git clone https://github.com/indes/flowerss-bot && cd flowerss-bot
make build
./flowerss-bot
```



## 配置

根据以下模板，新建 `config.yml` 文件。

```yml
bot_token: XXX
#多个telegraph_token可采用数组格式：
# telegraph_token:
#  - token_1
#  - token_2
telegraph_token: xxxx
preview_text: 0
disable_web_page_preview: false
socks5: 127.0.0.1:1080
update_interval: 10
error_threshold: 100
telegram:
  endpoint: https://xxx.com/
mysql:
  host: 127.0.0.1
  port: 3306
  user: user
  password: pwd
  database: flowerss
sqlite:
  path: ./data.db
```

配置说明：

| 配置项                     | 含义                                      | 是否必填                                       |
| --------------------------| ----------------------------------------- | ------------------------------------------ |
| bot_token                 | Telegram Bot Token                        | 必填                                       |
| telegraph_token           | Telegraph Token, 用于转存原文到 Telegraph   | 可忽略（不转存原文到 Telegraph ）          |
| preview_text              | 纯文字预览字数（不借助Telegraph）            |可忽略（默认0, 0为禁用）
| disable_web_page_preview  | 是否禁用 web 页面预览                       | 可忽略（默认 false, true 为禁用）          |
| update_interval           | RSS 源扫描间隔（分钟）                      | 可忽略（默认 10）                          |
| error_threshold           | 源最大出错次数                              |可忽略（默认 100）                          |
| socks5                    | 用于无法正常 Telegram API 的环境            | 可忽略（能正常连接上 Telegram API 服务器） |
| mysql                     | MySQL 数据库配置                           | 可忽略（使用 SQLite ）                     |
| sqlite                    | SQLite 配置                               | 可忽略（已配置mysql时，该项失效）          |
| telegram.endpoint         | 自定义telegram bot api url                | 可忽略（使用默认api url）          |