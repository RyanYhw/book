# Linux

## 便签

Indicator Stickynotes

```
sudo add-apt-repository ppa:umang/indicator-stickynotes
sudo apt-get update 
sudo apt-get install indicator-stickynotes 
```

## 配置ss客户端

```
sudo apt install shadowsocks
nohup slocal  -c shadowsocks/config.json &

// config.json 配置参考如下
{
    server: "IP",
    server_port :29468 ,
    local_address : "127.0.0.1",
    local_port : 1080,
    password: "",
    timeout:300,
    method: "AES-256-CFB"
}

pip install -U genpac // 安装genpac, 默认安装在 ~/.local/bin目录下

// 产生autoproy.pac 
~/.local/bin/genpac --pac-proxy="SOCKS5 127.0.0.1:1080" -o autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"

在系统网络VPN中将Network Proxy 设置为自动， URL设置为全路径的autoproxy.pac, 如/home/ryan/Documents/ss/autoproxy.pac

```