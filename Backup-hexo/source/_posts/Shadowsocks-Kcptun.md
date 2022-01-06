---
title: Shadowsocks-Kcptun
date: 2020-03-08 22:29:49
tags:
    - 科学上网
categories:
    - Linux
---
## Server

### Step 1、安装Docker

```shell
curl https://get.docker.com > docker_install.sh
bash docker_install.sh
systemctl start docker
```

### Step 2、 运行科学容器

<!--more-->

```shell
docker run -dt --restart=always --name $name -p 10001:6443 -p10001:6443/udp -p 20001:6500/udp mritd/shadowsocks -m "ss-server" -s "-s 0.0.0.0 -p 6443 -m aes-256-cfb -k $password --fast-open -u" -x -e "kcpserver" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2 --key $kcpPassword"
```

> `$`开头的为自定义信息


## Client


### Win

-  **shadowsocks-windows**

   - `https://github.com/shadowsocks/shadowsocks-windows`
   -  如何使用：
      - `https://github.com/shadowsocks/shadowsocks-windows/issues/1847`

- **kcptun插件**

  - `https://github.com/shadowsocks/kcptun`


- **参数设置：**

  ![YDVI1H](https://upyun.oneone.life/uPic/YDVI1H.png)


  - 插件程序：

    - 插件选项中输入 `client_windows_amd64` 的全路径
        > Win系统

  - 插件选项：

    - `dscp=20001;mode=fast2;key=$key;mtu=1350`
      > `$key`，替换为容器中配置的密码

### Mac

-  **shadowsocks-MacOS**

    - `https://github.com/yangfeicheung/Shadowsocks-X/releases`
- kcptun & 参数配置参考`Win`配置

### Android

- **shadowsocks-android**
  - `https://github.com/shadowsocks/shadowsocks-android`

- **kcptun-android**
  - `https://github.com/shadowsocks/kcptun-android`


- **参数配置：**
  - 参考win配置

