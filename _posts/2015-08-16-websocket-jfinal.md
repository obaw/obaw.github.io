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
最近用`JFinal`开发中使用了`WebSocket`，发现`WebSocket`总是建立不起连接，后来发现应该是`jfinal过滤器`把`websocket`请求过滤掉了。解决办法就是在`jfinal`的`config`中配置：
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

