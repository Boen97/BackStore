### email intro

1. email 在互联网初期就存在，并且一直到现在都是最重要和最流行的应用
2. email 是一个 asyncchronous communication medium 异步通讯媒介

### high overview of email system and its key components
1. key components
   1. user agent 例如qq邮箱客户端
   2. mail server 邮件服务器
   3. SMTP 协议 (Simple Mail Transfer Protocol)
   
   > 假设用户A要给用户B发送邮件，用户A首先在她的邮件客户端（user agent）编辑邮件，编辑完成点击提交之后
   > user agent 将邮件提交到 mail server 的 outgoing message queue
   > 最终邮件投递到用户B的 mail server, B想看的时候只要去 mail server 获取就行了
   
### SMTP 协议是email在应用层最主要的协议