### how popular video streaming services are implemented

#### quick view of video
1. a video is a subquence of images, displayed at a constant rate,eg 24 or 30 images per second
2. a video can be compressed to any bit rate

- from the networking perspective, the most challenge of video is **high bit rate**
- 100kbps ~ 4Mbps
- 4K video more than 10Mbps
- 2Mbps 的video 播放67分钟，消耗将近1Gb的存储和网络流量
- compressed to different version of video

### HTTP streaming and DASH
1. video is a file stored in a server
3. client use HTTP to request chunks of the video
4. But HTTP has a major shorcomming:
   all the client receive the same rate of video,whick is bad for low bandwidth client
5. DASH (Dynamic Adaptive Streaming over HTTP) 协议因此出现
   1. manifest file
      该文件记录了一个视频不同版本的列表信息，客户端获取到该文件后，能够自动选择适应它的视频版本
      
### Content Distribution Newworks
- the challenges of vido distribution
  1. distance to client
  2. a popular movie could be sent many times over same link, whick waste bandwidth
  3. single point of failure

> CDN 管理着位于世界各地的服务器，每个服务器存储着数据的副本，并且能够主动将用户的请求转发到最适合用户的服务器

- there could be private CDN and third-party CDN

- CDN server place ways:
  1. Enter Deep 在每一个ISP附近架设服务器，优点是离用户足够近，缺点是高度分散，不容易管理
  2. Bring Home 在 IXP 架设服务器，IXP 是多个 ISP 交换数据的地方，较第一种方式更为集中，管理起来更加方便，但是会有更高的延迟和更低的带宽
  
- Pull not Push
  CDN 不会在每一个集群上都存储备份，而是采用 Pull 的策略，当有 client 请求资源时再进行资源的缓存，这样资源将会尽可能得用在最需要缓存的资源上
  另外在缓存资源满的时候，优先删除最少使用的资源

