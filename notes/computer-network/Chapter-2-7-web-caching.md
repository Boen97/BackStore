# Web caching

- web cache also named **proxy sever** 代理服务器，正向代理，就是代理服务器

- forward proxy VS reverse proxy 正向代理和反向代理的区别
  > 具体可参考这篇文章 [What is a reverse proxy?](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/)
  1. 正向代理位于客户端，反向代理位于服务端
  2. 正向代理代理了客户端发出的请求，隐藏了客户端
  3. 反向代理代理了服务端发出的请求，向客户端隐藏了服务器的实际地址
  4. 简而言之，正向代理在代理客户端，反向代理代理服务端h

- 使用web cache的好处
  1. 从客户端的角度
    - 加快了访问速度
  2. 从服务器的角度
    - 减轻了服务器的压力，因为减少了实际的请求数量，很多请求在web cache中被缓存

- 实际缓存的 hit rates 从0.2 到 0.7不等

- web cache 的典型例子 CDN （content distribution networks）
  1. shared CDNs 和 dedicated CDNs

- The Conditional GET
  - 缓存中需要解决的一个很大的问题就是，缓存的一致性及缓存是否过期
  - HTTP提供了一个机制来解决缓存更新的问题：
    1. 服务器返回目标对象的时候会包含 Last-Modified 字段来标识对象上次修改的时间
    2. web cache服务器会定期 发送Conditonal GET 请求来校验缓存是否过期
      - Conditional GET
        1. HTTP GET 请求
        2. 包含 If-Modified-Since 字段
    3. 发送了Conditional GET请求后，如果请求对象更新了，那么服务器就会将最新的对象发送到缓存更新
    4. 如何没有更新，则会返回 304 Not Modified 状态码