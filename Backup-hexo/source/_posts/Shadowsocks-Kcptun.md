---
title: Shadowsocks & Kcptun  | v2ray
date: 2020-03-08 22:29:49
tags:
    - 科学上网
categories:
    - Linux
---
## SS & kcptun
### Server

#### Step 1、安装Docker

```shell
curl https://get.docker.com > docker_install.sh
bash docker_install.sh
systemctl start docker
```
国内极速下载：
`curl -sSL https://get.daocloud.io/docker | sh`

Docker 国内镜像源：
```shell
# vi /etc/docker/daemon.json
{
    "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
systemctl restart docker.service
```
#### Step 2、 运行科学容器

```shell
docker run -dt --restart=always --name $name -p 10001:6443 -p10001:6443/udp -p 20001:6500/udp mritd/shadowsocks -m "ss-server" -s "-s 0.0.0.0 -p 6443 -m chacha20-ietf-poly1305 -k $password --fast-open -u" -x -e "kcpserver" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2 --key $kcpPassword"
```

> `$`开头的为自定义信息

![此处输入图片的描述][1]

### Client

#### Win

-  **shadowsocks-windows**
![Shadowsocks.exe-2350kB][2]
   - `https://github.com/shadowsocks/shadowsocks-windows`
   -  如何使用：
      - `https://github.com/shadowsocks/shadowsocks-windows/issues/1847`

- **kcptun插件**
![client_windows_amd64.exe-3475.5kB][3]
  - `https://github.com/shadowsocks/kcptun`

    

  

- **参数设置：**

    ![image.png-140.3kB][4]

  - 插件程序：

    - 插件选项中输入 `client_windows_amd64` 的全路径
    > 例如：`D:\00_wuyh\AWS-Key\client_windows_amd64.exe`

  - 插件选项：

    - `dscp=20001;mode=fast2;key=$key;mtu=1350`
    > 把`$key`替换为所配置的`密码`

    

#### Android

- **shadowsocks-android**
  - `https://github.com/shadowsocks/shadowsocks-android`
![shadowsocks-arm64-v8a-4.8.4.apk-4702.3kB][5]
- **kcptun-android**
  - `https://github.com/shadowsocks/kcptun-android`
![kcptun-arm64-v8a-1.0.0.apk-3913.8kB][6]

- **参数配置：**
  - 参考win配置

---

## v2ray

`v2ray`一键安装/卸载脚本

```shell
sudo -i
bash <(curl -s -L https://git.io/v2ray.sh)
```

- 直接运行上面的脚本，选择`1`进行安装

    ![](https://upyun.oneone.life/upyun-img/20210406144842.png)

- 选择传输协议，根据自己需要进行选择（我这里只接用的默认`tcp`，回车即可）
    
    ![](https://upyun.oneone.life/upyun-img/20210406144904.png)

- 配置端口和广告拦截，根据自己需求来配置，如果使用默认回车即可

    ![](https://upyun.oneone.life/upyun-img/20210406144936.png)

- 配置是否开启`Shadowsocks`，开启则选`Y`，然后配置相关参数

    ![](https://upyun.oneone.life/upyun-img/20210406145053.png)
    
- 配置完成之后会打印出`V2Ray`和`Shadowsocks`的配置参数（使用`v2ray url`命令可以输出vmess URL链接方便一键导入到客户端中），然后把这些参数配置到对应的客户端（打印信息中有v2ray客户端的下载地址）中即可开始科学上网啦

    ![](https://upyun.oneone.life/upyun-img/20210406145250.png)

    ![](https://upyun.oneone.life/upyun-img/20210406145332.png)

- 在命令行直接输入`v2ray`命令可以显示出功能菜单

    ![](https://upyun.oneone.life/upyun-img/20210406145412.png)



### 客户端

#### Windows

`https://github.com/2dust/v2rayN/releases/latest`

#### Mac

`https://github.com/insisttech/v2rayX-copy/releases`

#### Android

`https://github.com/2dust/v2rayNG/releases`

## SwitchyOmega配置
SwitchyOmega是Chrome浏览器上的代理扩展插件,根据预先设置好的代理规则，轻松快捷的管理和智能切换多个代理设置
> 比较适合linux环境下使用，因为目前linux环境下的SS没有PAC配置，也没有SS的图形工具，所以建议`SwitchyOmega + shadowsocks`的方式

### 安装

直接从浏览器的应用商店中安装，或者直接从`github`上下载：

`https://github.com/FelisCatus/SwitchyOmega/releases `

### 配置

1. 配置代理服务器

    ![image.png-56.4kB][7]
    
2. 配置自动切换规则

    ![image.png-157.4kB][8]
    
    > 规则列表网址：`https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt`
    
3. 使用

    ![image.png-15.2kB][9]
    
    > 如果看到浏览器上的SwitchyOmega 图标有显示黄色感叹号，可以直接点击“1个资源未加载”项按提示操作即可，操作完，可看到切换规则处有新添对应规则。


  [1]: https://ws1.sinaimg.cn/large/7eff6b59gy1g79m4pr5vej21fq048aa9.jpg
  [2]: http://static.zybuluo.com/AlexWuYh/qdy26d0hnhf55rxsosay5q3u/Shadowsocks.exe
  [3]: http://static.zybuluo.com/AlexWuYh/11hjn4o1bxxdnt5u5e8xa03x/client_windows_amd64.exe
  [4]: https://upyun.oneone.life/uPic/YDVI1H.png
  [5]: http://static.zybuluo.com/AlexWuYh/2gkt93yhg57f1kv2bq3vvyi7/shadowsocks-arm64-v8a-4.8.4.apk
  [6]: http://static.zybuluo.com/AlexWuYh/1x6nnarcc0lph5prexjj4e4o/kcptun-arm64-v8a-1.0.0.apk
  [7]: https://upyun.oneone.life/upyun-img/20210129185742.png
  [8]: https://upyun.oneone.life/upyun-img/20210129185942.png
  [9]: https://upyun.oneone.life/upyun-img/20210129190058.png

