## http缓存

### 缓存介绍

> 缓存就是为了提高网站的性能，较少等待时间和网络的流量

### 缓存分类

> 通过使用cache-control来控制，cache-control属于通用首部，可以在请求头和响应头中使用

**共享缓存【cache-control: private】**

**定义**：多个用户可以访问的缓存【一般在代理服务器上】，

**私有缓存【cache-control: public】**

**定义**：单个用户能访问到，缓存在本地浏览器中，这些缓存为浏览过的文档提供向后/向前导航，保存网页，查看源码等功能，可以提供缓存内容的离线浏览。

### 缓存控制

> 通过cache-control来控制，请求头和响应头中都支持这个属性

- 不缓存：no-store

- 缓存但需要验证：no-cache 每次缓存都会将请求发送到服务端，进行校验，没有过期返回304，没有响应实体，过期了，返回最新的数据
- 私有和公共缓存：private、public
- 过期：max-age，比如max-age=31536000，代表失效周期
- 验证方式：must-revalidate  当浏览器使用陈旧资源的时候，必须进行校验，过期不再使用陈旧资源

### 协商缓存

缓存只有有限的空间用于存储资源副本，所以缓存会定期地将一些副本删除，这个过程叫做缓存驱逐。

当服务器上面的资源进行了更新，那么缓存中的对应资源也应该被更新，由于HTTP是C/S模式的协议，服务器更新一个资源时，不可能直接通知客户端更新缓存，所以双方必须为该资源约定一个过期时间，在该过期时间之前，该资源（缓存副本）就是新鲜的

当过了过期时间后，该资源（缓存副本）则变为陈旧的*。*

驱逐算法用于将陈旧的资源（缓存副本）替换为新鲜的，注意，一个陈旧的资源（缓存副本）是不会直接被清除或忽略的，

当客户端发起一个请求时，缓存检索到已有一个对应的陈旧资源（缓存副本），则缓存会先将此请求附加一个**`If-None-Match`**头

然后发给目标服务器，以此来检查该资源副本是否是依然还是算新鲜的，若服务器返回了 [`304`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/304) (Not Modified)（该响应不会有带有实体信息），则表示此资源副本是新鲜的，这样一来，可以节省一些带宽。

若服务器通过 If-None-Match 或 If-Modified-Since判断后发现已过期，那么会带有该资源的实体内容返回。

+ 如果资源请求的响应头里含有**ETag**：hash值, 客户端可以在后续的请求的头中带上 [`If-None-Match`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match) 头来验证缓存
+ 如果响应头里含有**`Last-Modified`**：Date值，客户端可以在后续的请求中带上 [`If-Modified-Since`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Modified-Since) 来验证缓存。

> 如果if-none-match和if-modified-since同时存在，if-modified-since会被忽略，因为ETag是强校验

### Vary

> 在响应头中的一个字段，用来决定后续的请求，是服务端回复还是缓存回复



