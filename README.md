# Heroku-vless

## 概述
Heroku是一个支持多种编程语言的云平台即服务。目前支持Ruby、Java、Node.js、Scala、Clojure、Python、PHP和Perl等语言，基础操作系统是Debian。

本项目用于在 Heroku 上部署 vless+websocket+tls，每次部署自动选择最新的 alpine linux 和 xray core。相比vmess，vless的性能更加优秀，占用资源更少，运行更加稳定。

刚测试了一下，herokuapp.com这个域名已经被墙（2021.9.27），故现在如果不配置cf流量中转，这个将无法使用，建议使用cloudflare的workers的流量中转，速度更快，原则上不会有被墙风险。

## 镜像

经测试本镜像占用内存资源较低，运行稳定。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Frptec%2Fheroku-vless)

## 注意

### 路径

`WebSocket` 路径(配置文件中的 `path` )为 `/` 。你也可以自行修改

### 端口

`端口` 为 `443` 。 


### UUID

`UUID` 默认为 `10974d1a-cbd6-4b6f-db1d-38d78b3fb109` 你也可以在部署时自由修改（建议修改）。

## 流量中转

使用cloudflare的workers来`中转流量`，配置为： 

```
addEventListener(
      "fetch",event => {
         let url=new URL(event.request.url);
         url.hostname="你的heroku域名.herokuapp.com";
         let request=new Request(url,event.request);
         event. respondWith(
           fetch(request)
         )
      }
    ) 
```


详细教程
https://92km.net/archives/VLESS-Heroku-cloudflareworkers.html

如果你觉得heroku 速度太慢，不支持netflix等流媒体解锁，你也可以试试使用付费的，例如vultr等
使用下面链接会有赠送100刀（以前可以充值5刀，用1年多，现在似乎只能用两个月）
https://www.vultr.com/?ref=8446608-6G

