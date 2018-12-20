# 术语

Terms specific to the Dat software.

### dat, Dat archive, archive

Dat，或者说是Dat存档（Dat archive），就是一堆文件加上一个dat元数据文件 (see [SLEEP](#sleep))。 dat文件夹可以包含任何文件，它们都可以同步到其他用户那里。 每个dat都有一个dat链接用于分享。

在你创建一个新的dat时,其实你也创建了一个 `.dat` 文件夹用来存放dat元数据和秘钥(a public and secret key).

### 秘钥（Secret Key）

用于分享的Dat链接是秘钥对的一部分（后半部分）。 拥有完整秘钥的用户就可以获得对dat的编辑权限了（可以修改或分享）。

使用命令行或桌面应用的话，秘钥会存储在home目录 `~/.dat/secret_keys`。如果你要换新电脑的话，一定要备份秘钥！

### （编辑者）Writer

可以编辑某个dat的用户。编辑者拥有完整的秘钥，秘钥允许他进行编辑。目前dats支持单人编辑。

### Collaborator

被某dat所有者授权浏览的用户。 如果某个dat的所有者或其他的collaborator把dat链接分享给你，你就可以进行浏览或下载了。

未来，Dat计划支持用户授权其他collaborator编辑，更改dat或在dat中创建新文件。

### Swarm or Network

通过分布式网络（p2p）互联并下载了dat的一组对等节点。

## General Terms

### 分布式网络（Distributed Web）

在分布式网络（p2p）模型中，用户在下载数据的同时也会提供提供带宽分享数据。分布式网络有越多的人加入，就会变得更快，更安全，还有更多冗余。

目前，互联网还是集中式的。如果有人控制了硬件或者通讯线路，他们就能控制网站上所有的用户。[Read more here](http://brewster.kahle.org/2015/08/11/locking-the-web-open-a-call-for-a-distributed-web-2/)
### Peer to Peer (p to p)

p2p程序会在p2p网络上搜索所有其他连接到该p2p网络的计算机来定位其需要的内容。 The peers of such networks are end-user computer systems that are interconnected via the Internet.

在Dat中， 只用拥有相同链接的用户才可能互相连接。

### Secure Register

这个 [register]( https://gds.blog.gov.uk/2015/09/01/registers-authoritative-lists-you-can-trust/) 是一个权威可信任的信息列表。 我们维护了一个叫做[Dat Folder](https://datproject.org) 的开放寄存处，它是对任何人开放的。

### Beaker

 [Beaker Browser](https://beakerbrowser.com/)是一个实验性p2p浏览器，它既可以像传统浏览器一样浏览网站，也可以查看或发布dat。

## Technical Terms

### SLEEP

SLEEP is the the on-disk format that Dat produces and uses. It is a set of 9 files that hold all of the metadata needed to list the contents of a Dat repository and verify the integrity of the data you receive.

The acronym SLEEP is a slumber related pun on REST and stands for Syncable Lightweight Event Emitting Persistence. The Event Emitting part refers to how SLEEP files are append-only in nature, meaning they grow over time and new updates can be subscribed to as a realtime feed of events through the Dat protocol.

Read the full [SLEEP specification](https://github.com/datproject/docs/blob/master/papers/dat-paper.md#3-sleep-specification) in the dat whitepaper.

### Key

A 32-bit hash that uniquely represents a feed. All feeds have keys. The metadata key is used as the public key for an archive.

### Public Key vs Secret Key

The public key is the key that is shared in the Dat Link. Messages are signed using the secret key, allowing write access to feeds. The owner is the only user with the secret key.

### Discovery Key

The discovery key is a hashed public key. The discovery key is used to find peers on the public key without exposing the original public key to network.

### Feed

A feed is a term we use interchangeably with the term "append-only log". It’s the lowest level component of Dat. For each Dat, there are two feeds - the metadata and the content.

Feeds are created with hypercore.

### Metadata Feed

就像HTTP的header一样, 元数据包含了一个指向dat中文件的指针和一个文件列表。

The metadata is a hypercore feed. The first entry in the metadata feed is the key for the content feed.

### Content Feed

The content feed is a hypercore feed containing the file contents for a Dat archive. The content feed together with a metadata feed make a Dat archive.

### Hyperdrive

[Hyperdrive](https://github.com/mafintosh/hyperdrive) is peer to peer directories. We built hyperdrive to efficiently share scientific data in real time between research institutions. Hyperdrive handles the distribution of files while encrypting data transfer and ensuring content integrity. Hyperdrive creates append-only logs for file changes allow users to download partial datasets and to create versioned data. Hyperdrive is built on hypercore.

Archives created with hyperdrive are made with two feeds, one for the metadata and one for the content.

### Hypercore

[Hypercore](https://github.com/mafintosh/hypercore) 是一个分发、复制二进制数据提要的协议。 它可以建立一个高效的消息网络来将延迟降到最低。 Hypercore 是一个一致的、可用性极高、允许分区的系统。
