# wx-login-demo
基于网页授权的微信扫码登录Demo

## 使用技术
- vue:2.6.11
- vuex:3.1.2
- vue-router:3.1.5
- vue-qr:2.2.1
- element-ui:2.13.0
- vant:2.5.3
- koa:2.11.0
- mongodb:3.6.0

## Demo演示
<http://scancode.xuedingmiao.com>

## 安装

### web端
env配置
```
ENV = 'development'
VUE_APP_BASE_API = 'http://localhost:2000'

#appid 可填入申请的测试公众号id或者其它准备好的ID
VUE_APP_WECHAT_APPID=''

#authUrl 网页授权中间页
VUE_APP_WECHAT_AUTH_URL='自己的域名/auth.html'
```
项目部署到服务器上之后可访问auth.html(即public目录下的auth.html)

安装依赖
```
npm install
```

开发
```
npm run serve
```

访问
```
http://localhost:9555
```
web端默认使用9555端口

### 公众号配置(不要忘记)
- 授权回调页面域名
    - 项目基于网页授权实现的扫码登录，所以需要在公众号管理后台修改网页授权获取用户基本信息的 **[授权回调页面域名](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html)** 
- 模板消息
    - 如果需要发送登录模板消息则要添加下可用的登录提醒模板

### 服务端
- koa
- mongodb(阿里云公开镜像)  

执行```run-mongo.sh```脚本完成mongodb容器启动  
创建数据库runoob(可使用adminmongo图形化界面操作)

安装依赖
```
cd server
npm install
```

配置公众号，复制一份config.sample.js重命名为config.js填好如下配置  
```js
module.exports = {
  db: '', // mongodb的连接地址
  url: '', // 模板消息点击跳转地址
  template_id: '', // 模板消息ID
  appId: '', // 公众号appid
  appSecret: '' // 公众号secrect
}
```

启动服务
```
node app.js
```

访问地址
```
http://localhost:2000
```

之前研究了下微信端扫码登录的实现微信网页扫码登录和公众号网页授权登录的比较。
因为微信开放平台的扫码登录需要认证(交钱)，就稍微麻烦一点使用网页授权的方式来做 PC 端扫码登录。

实现思路
简要介绍

PC 端点击扫码登录时会生成一个 uuid 并弹出一个二维码，二维码地址(附带了生成的 uuid)是移动端的网页，微信扫码后打开的是配置好的网页授权链接，通过网页授权的方式获取 code 拿到用户 openid 或者 unionid 后存入数据库中，PC 端通过轮询方式根据生成的 uuid 作为参数来获取用户 id 进行登录

涉及技术
vue:2.6.11

vuex:3.1.2

vue-router:3.1.5

vue-qr:2.2.1

element-ui:2.13.0

vant:2.5.3

koa:2.11.0

mongodb:3.6.0

web 端
env 配置

ENV = 'development'
VUE_APP_BASE_API = 'http://localhost:2000'

#appid 可填入申请的测试公众号id或者其它准备好的ID
VUE_APP_WECHAT_APPID=''

#authUrl 网页授权中间页
VUE_APP_WECHAT_AUTH_URL='自己的域名/auth.html'
项目部署到服务器上之后可访问 auth.html(即 public 目录下的 auth.html)

安装依赖

npm install
开发

npm run serve
访问

http://localhost:9555
web 端默认使用 9555 端口，可以修改为其它端口。

服务端
数据库服务由 mongodb 的 docker 镜像提供，如果已经安装了 docker 则可通过项目下的脚本启动容器

koa

mongodb(阿里云公开镜像)

执行run-mongo.sh脚本完成 mongodb 容器启动
创建数据库 runoob(可使用 adminmongo 图形化界面操作)

安装依赖

cd server
npm install
修改公众号配置，复制一份 config.sample.js 重命名为 config.js 填好如下配置

module.exports = {
  db: '', // mongodb的连接地址
  url: '', // 模板消息点击跳转地址
  template_id: '', // 模板消息ID
  appId: '', // 公众号appid
  appSecret: '', // 公众号secrect
}
启动服务

node app.js
访问地址

http://localhost:2000
服务端接口使用 2000 端口

公众号配置
授权回调页面域名

项目基于网页授权实现的扫码登录，所以需要在公众号管理后台修改网页授权获取用户基本信息的 授权回调页面域名

模板消息

如果需要发送登录模板消息则要添加下可用的登录提醒模板

在线 Demo
http://scancode.xuedingmiao.com


效果演示




参考文档：

授权回调页面域名：

https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html

微信网页授权：

https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html

网站应用微信登录

https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html

github:

https://github.com/xuedingmiaojun/scan-login-demo


服务端接口使用2000端口

![](https://visitor-badge.glitch.me/badge?page_id=xuedingmiaojun.scan-login-demo)

