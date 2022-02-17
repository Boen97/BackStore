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