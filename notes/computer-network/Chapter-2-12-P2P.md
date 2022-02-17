## Peer to Peer File Distribution

> not like web, email, DNS are client-server architectures, rely on always-on infrastrucure
> P2P are interconnected peers, communicate with each other directly

large file distribution example

1. client-server architectures
   the server consuming a lot of bandwidth and resource
2. P2P architectures
   each peer could redistribution any portion of the file it has recevied to any other peers

- P2P vs client-server
  client-server 服务器的上传能力仅仅为服务器本身
  P2P 中的每个节点都参与了上传，因此上传能力相当于每个节点 Peer 的上传能力之和,因此，随着节点数量的增加，P2P 可以实现自适应，有很强的自我扩展性 

- BitTorrent 中几个有意思的概念
  1. chunk
     peer 之间传输的块大小，为 256 KBytes
  2. peer
     参与传输的节点
  3. tracker
     peer 的注册中心，每个peer可以从这获取相邻的 peer 节点
  4. rarest first
     最稀有的块优先参数交易与传输
  5. unchoked
     相当于候选的optimistically unchoked 节点
  6. optimistically unchoked
     每个节点有自己的top4交易节点，这些top节点优先参与交易
  7. choked
  8. tip-for-tat 一报还一报
  9. DHT (Distributed Hast Table) 分布式表
  