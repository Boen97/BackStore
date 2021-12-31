# User-Server Interaction: Cookies

- Cookies 技术由四部分内容组成
  1. a cookie header line in the request message
  2. a cookie header line in the response message
  3. a cookie-file kept on the user's end system
  4. 网站后端的数据库

- 每个网站有一个cookie-file文件
- 使用cookie的具体过程如下：
  1. 用户首次向服务器发起请求
  2. 服务器返回的response message 中包好 set-cookie 字段，里面存储了需要保存在 cookie 文件中的内容
  3. 客户端浏览器将set-cookie字段中的内容追加到cookie文件里
  4. 客户端再次发起请求的时候，在request message中带上cookie字段用来表明身份
  - 服务器在数据库中会维持cookie与实际用户信息的映射
