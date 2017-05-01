---
layout:     post
title:      "JFinal过滤掉WebSocket请求解决办法"
subtitle:
date:       2015-08-16 16：00：00
author:     "Obaw"
catalog:    false
header-img: ""
tags:
    - Java
address: 捡人网络
---
最近用JFinal开发中使用了WebSocket，发现WebSocket总是建立不起连接，后来发现应该是jfinal过滤器把websocket请求过滤掉了。解决办法就是在jfinal的config中配置：
```java
@Override
public void configHandler(Handlers me) {
     me.add(new ContextPathHandler("base"));
     me.add(new UrlSkipHandler("/websocket", false));
}
```
这里是websocket服务
```java
@ServerEndpoint("/websocket")
public class LoginListener {

    @OnMessage
    public void onMessage(String uuid, Session session) throws IOException, InterruptedException {
    }
}
```

