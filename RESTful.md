## RESTfull**规范**

REST的全称是`Resource Representational State Transfer`，即资源表现形式的状态转移（或者说是状态变化）。**资源即数据，他们以HTML、XML、JSON、PNG等等形式表现出来，然后通过HTTP的增删改查动词（POST、DELETE、PUT、GET）操作来对它们进行操作，来改变它们的状态。

用某大佬的一句话概括就是
```
URL定位资源，用HTTP动词（GET,HEAD,POST,PUT,PATCH,DELETE）描述操作，用响应状态码表示结果
```
其实就是面向资源的、对URI进行暴露的一种规范，通俗的概括就是
```
看Url就知道要什么
看http method就知道干什么
看http status code就知道结果如何
```

## 详细解释

REST的官方翻译应该是：`表述层状态转移`，是一个结构简单、伸缩性强、松耦合的Web架构风格。

#### REST涉及的几个关键词
* 资源（Resource）：内容数据
* 资源的表述（Representational）：数据的展现形式，如HTML、JSON、PNG等
* 状态转移（State Transfer）：在客户端和服务端之间转移代表资源状态信息的表述
* 统一接口（Uniform Interface）：HTTP七大动作、统一的HTTP头信息、状态码、缓存机制、身份认证机制

#### RESTful的约束或特点
1. 客户端-服务器（Client-Server）<br>
客户端、服务端分离，这样可以简化服务器，并且可以前后端分别优化
1. 无状态（Stateless）<br>
会话状态应该全部由客户端维护，从客户端发出的请求应当包含服务端所需的所有信息，这样降低了服务器的资源使用，服务端也可以单独考虑每个请求。
1. 缓存（Cachable）<br>
服务器返回信息必须被标记是否可以缓存，如果缓存，客户端可能会重用之前的之前的资源。这样可以减少交互次数，来节省网络资源；并且降低了延迟
1. 分层系统（Layered System）<br>
中间层封装，系统某层不需要知道与它相邻层之外的事情。降低了系统的复杂度。
1. 统一接口（Uniform Interface）<br>
提高可见性，降低耦合性
1. 按需代码（Code-On-Demand，可选）<br>
支持通过下载代码来执行，提高可扩展性）


#### RESTful必须满足安全性和幂等性
RESTful规范必须满足HTTP的安全性和幂等性

> 对HTTP协议的使用实际上存在着两种不同的方式：一种是RESTful的，它把HTTP当成应用层协议，比较忠实地遵守了HTTP协议的各种规定；另一种是SOA的，它并没有完全把HTTP当成应用层协议，而是把HTTP协议作为了传输层协议，然后在HTTP之上建立了自己的应用层协议。

| HTTP Method | 幂等性  | 安全性 |
| ----------- |:-------:|:------:|
| OPTIONS |yes |yes             |
| GET |yes|yes                  |
| HEAD|yes|yes                  |
| PUT |yes|no                   |
| POST|no |no                   |
| DELETE|yes |no                |
| PATCH |no  |no                |

###### 安全性
不改变资源表述的方法，它仍然可能改变服务器上的内容或资源，但这必须不导致不同的表现形式。比如DELETE是安全的，但下面这样的API明显不符合安全性
```
GET /blog/1234/delete HTTP/1.1
```
安全方法是那些可以被缓存、对资源无损预加载的方法。

###### 幂等性
HTTP 幂等方法是指无论调用1次还是N次都有同样结果的 HTTP 方法。幂等对于构建一个容错能力强（fault-tolerent）的 API 非常重要。假设一个客户端希望通过 POST 来更新一个资源，由于 POST 是一个非幂等方法，调用它多次 将导致错误的更新。那么当你向服务发送一个 POST 请求过程中超时将会发生什么，是不是资源已经被更新？超时发生在向服务器发送请求阶段还是服务返回 客户端阶段？我们是否能够安全地重试一遍，或第一要查出资源究竟发生了什么变化？通过幂等方法，我们则无须回答这种问题，直到我们从服务器得到返回， 我们可以安全地重发请求。


#### 相关链接

[RESTful 手册][RESTful 手册]

[GitHub开发者REST API规范][GitHub REST API v3]

[撰写安全合格的REST API][撰写安全合格的REST API]

[RESTful API 设计指南][RESTful API 设计指南]

[理解HTTP幂等性][理解HTTP幂等性]




[RESTful 手册]: https://sofish.github.io/restcookbook/
[GitHub REST API v3]: https://developer.github.com/v3/media/#request-specific-version
[撰写安全合格的REST API]: https://zhuanlan.zhihu.com/p/20034107
[RESTful API 设计指南]: http://www.ruanyifeng.com/blog/2014/05/restful_api.html
[理解HTTP幂等性]: https://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html
