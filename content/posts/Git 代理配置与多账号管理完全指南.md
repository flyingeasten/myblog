---
title: Git代理配置与多账号管理完全指南
date: 2025-09-244, 10:07:42 上午
draft: true
tags: []
lastmod: 2025-09-245, 2:36:54 下午
categories:
---

> 一句话总结：无论用 HTTPS 还是 SSH 与远程仓库通信，都能通过「全局 + 仓库级」双层配置，干净地解决网络代理和多账号并存的问题。

---

## 一、HTTPS/HTTP 代理

- Git 通过 `http.proxy / https.proxy` 两个键值对控制所有基于 HTTPS/HTTP 协议的流量。  
- 配置分三层：`system > global > local`，优先级从左到右逐级覆盖。下文示例默认使用 `global` 与 `local`。

### 1. 全局代理（所有仓库生效）

```bash
# 1) HTTP/HTTPS 普通代理
git config --global http.proxy  http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

# 2) SOCKS v5（如 Shadowsocks/V2Ray）
git config --global http.proxy  socks5h://127.0.0.1:1080
git config --global https.proxy socks5h://127.0.0.1:1080
```

> `socks5h` 中的 `h` 表示让代理服务器解析域名，避免本地 DNS 污染。

### 2. 针对单一域名代理（仅 GitHub 走代理）

bash

复制

```bash
git config --global http.https://github.com.proxy  socks5h://127.0.0.1:1080
# 取消时置空即可
git config --global http.https://github.com.proxy ""
```

### 3. 查看与撤销

bash

复制

```bash
# 查看
git config --global --get-regexp proxy        # 一行一个键值
git config --global --list | grep proxy       # 等价写法

# 撤销
git config --global --unset http.proxy
git config --global --unset https.proxy
```

---

## 二、仓库级独立配置




---
## 一、git代理(proxy)设置

git连接远程仓库一般有两种方式，一种是HTTP/HTTPS，另一种是SSH，下面展开说明。

### HTTP/HTTPS代理命令：

#### 1.配置HTTPS 代理

```

# 配置全局 HTTP 代理
git config --global http.proxy http://127.0.0.1:1080

# 配置全局 HTTPS 代理
git config --global https.proxy https://127.0.0.1:1080

# 也可以使用 socks5 代理（如 Shadowsocks）
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080

```



#### 2. 只为特定域名配置代理

如果只想对 GitHub 等特定域名使用代理，可以这样设置：

```bash
# 只对 github.com 使用代理
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
git config --global https.https://github.com.proxy socks5://127.0.0.1:1080

# 对特定域名不使用代理
git config --global http.https://github.com.proxy ""
```

#### 3. 查看当前代理配置



```bash
# 查看所有代理相关配置
git config --global --get http.proxy
git config --global --get https.proxy

# 查看所有配置
git config --global --list
```

#### 4. 取消代理配置



```bash
# 取消全局 HTTP 代理
git config --global --unset http.proxy

# 取消全局 HTTPS 代理
git config --global --unset https.proxy

# 取消特定域名的代理
git config --global --unset http.https://github.com.proxy
git config --global --unset https.https://github.com.proxy
```

  

  
要为特定仓库设置独立的账号和代理（不影响全局配置），可以在该仓库目录下执行不带 `--global` 选项的 `git config` 命令，这些配置会保存在当前仓库的 `.git/config` 文件中。

### 为特定仓库配置独立账号


```bash
# 进入目标仓库目录
cd /path/to/your/repo

# 配置当前仓库专用的用户名
git config user.name "Specific Username"

# 配置当前仓库专用的邮箱
git config user.email "specific.email@example.com"
```

#### 为特定仓库配置独立代理


```bash
# 进入目标仓库目录
cd /path/to/your/repo

# 为当前仓库配置 HTTP 代理
git config http.proxy socks5://127.0.0.1:1080

# 为当前仓库配置 HTTPS 代理
git config https.proxy socks5://127.0.0.1:1080

# 也可以只为当前仓库的特定域名配置代理
git config http.https://github.com.proxy socks5://127.0.0.1:1080
```

#### 查看特定仓库的配置


```bash
# 查看当前仓库的所有配置（包括独立设置的账号和代理）
git config --list

# 查看当前仓库的用户信息
git config user.name
git config user.email

# 查看当前仓库的代理配置
git config http.proxy
git config https.proxy
```

#### 取消特定仓库的配置


```bash
# 取消当前仓库的用户名配置
git config --unset user.name

# 取消当前仓库的代理配置
git config --unset http.proxy
git config --unset https.proxy
```

  

  

#### 原理说明

- 不带 `--global` 选项的配置只作用于当前仓库，保存在仓库根目录的 `.git/config` 文件中
- 仓库级别的配置优先级高于全局配置，会覆盖全局设置
- 这种方式适合多账号开发场景（如同时维护个人项目和公司项目）

### SSH设置