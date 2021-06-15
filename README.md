# anti_sign逆向app集合
仅供学习，如有侵权，请告知。
最近逆向的app：中国移动、中国电信、微信


1. joyrun: 悦跑圈
2. tianyancha: 天眼查
3. caocao: 曹操专车
4. umetrip: 航旅纵横
5. varliflight: 飞常准
6. qichacha: 企查查
7. qixinbao： 启信宝

# 最近逆向
## 20200715
 微信，从app到pc端，一层一层分析，最后把聊天备份文件解析完成，包含Backup.db，BAK_0_TEXT和BAK_0_MEDIA，因为涉及到商业机密，我就只能说以下几点。
- Backup.db存储的是索引信息
- BAK_0_TEXT是消息内容集合，采用的是protobuf协议+AES加密存储
- BAK_0_MEDIA是所有媒体资源的集合。采用AES加密存储

QQ: 
- 数据库文件用了xxtea加密，符合QQ一贯作风，解密完后数据库是sqlite，随便打开。
- 消息内容用的protobuf存储，需要自己去猜测字段

近期想写个关于美团、淘宝客户端的抓包教程，这是一个很骚的操作，用到的是降级网络抓包。

## 20201023
搞potato chat的协议，前后断断续续搞了两个月，其实如果全身心搞，最多两个星期就可以搞出来。协议完全抄袭telegram，后续打算写个教程。

接下来准备搞微信协议，前期已经对tls1.3相关算法进行了充电，搞微信协议应该是个持续高难度工作。

## 20210126
最近研究抖音的x-gorgon签名生成，这个签名已经算是业界比较领先水平了。每次签名还不一样，打破了我常规的思路。有空分享一下解析过程。

## 20210615
搞了一段时间快手的协议，sig和__NStokensig计算方式很简单了，网上到处是公开了（安卓的salt和ios的salt不太一样，其他算法一致），只不过现在版本用sig都不行了。

新版新增了__NS_sig3，起初打算完全做算法还原，但对比了一下快手版本迭代，估计最多不到半年，算法就废了。6.8版本的sig3协议还原可以参考：https://bbs.pediy.com/thread-267857.htm

最后使用frida调用苹果手机的方案，用手机作为sig3计算器。测算了一下，一部iphone6，一天计算大几百万个sig3无压力。
