---
typora-root-url: ./
---

# Godzilla Suo5MemProxy Plugin

> 免责声明：此工具仅限于安全研究，用户承担因使用此工具而导致的所有法律和相关责任！作者不承担任何法律责任！

## 插件简介

关于Suo5MemProxy：

Godzilla Suo5MemProxy插件用于在Godzilla 连接java系统Webshell后可以基于当前中间件，通过注入内存马的方式实现一键化的注入Suo5内存代理，在隐蔽的同时提供更好的性能。



关于Suo5：https://github.com/zema1/suo5/tree/v0.9.0

**Suo5 一款高性能 HTTP 代理隧道工具**

suo5 是一个全新的 HTTP 代理隧道，基于 HTTP/1.1 的 Chunked-Encoding 构建。相比 Neo-reGeorg 等传统隧道工具, suo5 的性能可以达到其数十倍。

其主要特性如下：

- 同时支持全双工与半双工模式，传输性能接近 FRP
- 支持在 Nginx 反向代理和负载均衡场景使用
- 完善的连接控制和并发管理，使用流畅丝滑
- 支持 Tomcat Jetty Weblogic WebSphere Resin 等主流中间件
- 支持 Java4 ~ Java 19 全版本, 兼容性拉满
- 同时提供提供命令行和图形化界面



## 插件导入

![image-20230807232015174](/img/1.png)

配置->插件配置

![image-20230807232027214](/img/2.png)

进入插件管理面板后点击左下方添加按钮

![image-20230807101911370](/img/3.png)

选择下载好的Suo5Proxy.jar进行导入

![image-20230804134208161](/img/4.png)

提示插件导入成功

![image-20230807101939797](/img/5.png)

在PluginManage面板中能够成功显示插件路径则证明已成功导入。

![image-20230804134240243](/img/6.png)



## 插件使用

插件导入成功后，选择本地的测试Webshell，右键单击进入，进入到Webshell管理页面

![image-20230807232044742](/img/7.png)

导入插件后，可以在上方标签栏中找到`Suo5MemProxy`标签，单击可以进入到插件的功能面板

![image-20230804134543573](/img/8.png)

目前插件已经集成了Servlet、Filter两种类型的Suo5内存代理，通过注入内存马的方式将Suo5代理注入到WEB应用中

### 注入内存代理

**Servlet内存代理注入**

使用时可以根据目标中间件自行选择`PROXY_TYPE`与`URL_PATTERN`，内存代理类型(默认为Servlet)与映射路径(默认为`/favicon.ico`)，选好后点击`RUN`按钮，提示OK则注入成功。

![image-20230804135433107](/img/9.png)

可以到Godzilla内置的ServletManage插件中查看当前WEB容器中所有的servlet，发现路径为`/favicon.ico`的servlet，证明注入成功

![image-20230804140348112](/img/10.png)

使用Suo5代理客户端进行连接，成功连接到内存代理

![image-20230807232934526](/img/11.png)

使用Proxifier进行测试，可以成功通过代理请求到www.baidu.com

![image-20230807232951148](/img/12.png)

**Filter内存代理注入**

在`PROXY_TYPE`处，选择Suo5Filter，然后点击`Run`按钮进行注入

![image-20230804140752663](/img/13.png)

同样，提示OK则代表注入成功

![image-20230804140918232](/img/14.png)

可以到FilterShell插件getAllFilter进行查看/Suo5Filter111路由的代理是否注入成功

![image-20230804142828645](/img/15.png)

使用Suo5代理客户端进行连接，成功连接到内存代理

![image-20230807233728996](/img/16.png)

使用Proxifier进行测试，可以成功通过代理请求到www.baidu.com

![image-20230807233756217](/img/17.png)

### 卸载内存代理

**Servlet代理卸载**

卸载Servlet型内存代理只需要进入到`Suo5MemProxy`插件中，单击`UnLoadMemoryShell`按钮，在弹出的窗口中输入内存代理的路径(例如/favicon.ico)即可完卸载Servlet内存Suo5代理操作。

![image-20230804141307118](/img/18.png)

提示OK则说明卸载成功

![image-20230804141530828](/img/19.png)

可以来到ServletManger插件进行验证，/favicon.ico路由的Servlet已经被卸载

![image-20230804142542733](/img/20.png)

**Filter代理卸载**

Filter内存代理需要来到FilterShell插件进行卸载，首先getAllFilter，根据映射路由找到对应的Filter

![image-20230804142828645](/img/21.png)

由于卸载Filter内存代理需要用到Filtername，所以需要将对应的filtername复制到弹出的输入框中，然后点击确定即可完成卸载

![image-20230804143103878](/img/22.png)

再次点击getAllFilter按钮，发现内存代理已经成功卸载掉

![image-20230804143225395](/img/23.png)

## 参考

https://github.com/zema1/suo5/tree/v0.9.0

https://github.com/BeichenDream/GodzillaPluginDemo