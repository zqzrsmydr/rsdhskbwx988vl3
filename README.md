##一、Heroku部署程序
1、注册Heroku账号并登录，点击通过 https://dashboard.heroku.com 注册一个账号，不建议使用国内邮箱注册，例如QQ邮箱，163等！

 ![注册](https://img.21t.co/2021/06/15/72696a.png) 
 
2、注册成功以后登录，登录以后点击 

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Frptec%2Fheroku-vless)

地址：

```
https://dashboard.heroku.com/new?template=https://github.com/rptec/heroku-vless
```
3、你也可以在浏览器上复制上述地址部署应用！
其中App name你可以自由填写，UUID 为安全考虑，建议你自行替换掉我用的默认id。
点击 Deploy app 系统会自动部署。
 ![设置](https://img.21t.co/2021/06/15/d51bc9.png) 
4、部署完成以后，进入管理app，点击 Settings 再点击 Reveal Config Vars 就可以看见 UUID了！记下自己的UUID，后面马上会用到。
5、接着往下，你会看见Domains项后有个域名！https://*****.herokuapp.com/ 记下域名，稍后配置CloudFlare 反向代理会用到！（当然你如果不考虑速度的话，也可以不用配置cf代理）
##二、流量中转加速
配置CloudFlare反向代理加速v2！
1、首先登陆 [cloudflare官网](https://www.cloudflare.com/) ，然后点击 右侧的 Workers ！
 ![cf](https://img.21t.co/2021/06/15/0c3704.png) 

2、点击创建Workers

![创建](https://img.21t.co/2021/06/15/1a0c68.png)

3、复制下方代码，并添加进去！注意把下面的中文替换成你之前在Domains项看见的那个域名前缀
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

至此！部署完成了，你可以直接使用V2客户端！
##三、配置V2客户端
###1、客户端下载地址：
###WIN客户端
https://github.com/v2fly/v2ray-core/releases
###安卓客户端 
googleplay下载

[![Deploy](https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png)](https://play.google.com/store/apps/details?id=com.v2ray.ang)
直接下载
https://github.com/2dust/v2rayNG/releases
###IOS 
请自行下载小火箭等

###2、配置客户端。
请按照图片的要求设置！否则不能联网！
 ![设置](https://img.21t.co/2021/06/15/ed87c8.png) 

地址这里建议使用自选ip，速度可以拉满，具体参考我以前文章，或者自行baidu。

###3、youtube测速
 ![youtube](https://img.21t.co/2021/06/15/668c92.png) 

