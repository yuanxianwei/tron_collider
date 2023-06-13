### tron_collider 私钥探测碰撞器

### 举例 概率分析
我们先对碰撞比特币私钥进行概率分析

先获取我们有多少的比特币地址(持币地址 - 比特币BTC) - BTC.com 为全球区块链爱好者提供专业的数据与矿池服务)，我们可以看见大概有1000万左右比特币地址的余额在0.001比特币以上.而比特币的secp256k1的阶数正好近似于2^256的数目的(稍微低一点)那么我们平均需要扫描多少的地址才能有50%的概率出来一个地址呢?

根据生日攻击原理，这个数目就正好是一半，我们有1000个矿机。 2256=5.78960446 x106710000001000-2 N = 这个数字看上去还是有点大，在以太坊挑战赛里面，56位的被破解， 也就是说目前破解还是完全可能


### 分布式算法

虽然破解的概率还是很小，我们还是要讨论一下如果要写分布式破解算法怎么写?

我们这个计算过程有以下特点 1.只包含了三种运算: ECC运算，hash运算，数据查询运算 其中这三种运算用到的芯片恰好还不一样。ECC用的是CPU或者FPGA等等， 而hash运算存在专门256bitsASIC矿机进行快速运算，数据查询运算主要需要一块大内存。 ( 107=305MB) 8-10242 因为这三个机器的工作效率不同，且适合的机器也不同，因此我们采用如下的计划: ECC矿机950台，hash矿机10台，40台查询矿机。 ECC计算出的公钥运送到hash矿机，矿机再输送到查询矿机。 进一步软件优化 我们这里还有一些优化的空间 小学二年级学过椭圆曲线算法遵循以下规律 (m+n)P=mP+nP 因此对于每一个矿机我们可以对其分配一个240bit的地址，对于这个地址一次性挖取2^16个块 这样对于一个XP只需要进行+P操作就可以了 在hash矿机端还可以加上一个取secp256k1阶的负值 (#k1 - x)p = -zp 相当于对复杂度进行了mod2处理. 硬件优化 CC专用芯片有很多，但是专门针对secp256k1曲线的矿机为0. 开发的话，可以采用以下方法:预运算好 2P,3P,4P,8P....2255 P 到时候，可以直接进行点加运算

### 使用说明
此软件使用离线方式随机生成私钥地址，一个个地址去节点查询，当查询到该地址有交易记录时会自动停止，并把地址和私钥显示出来

### 支持多开
开机一天跑500万数据， 开机一个月跑一亿五千万。开机一年跑37亿数据。实现暴富不是梦

探测碰撞成功之后为

恭喜您，碰撞成功

地址： xxxxxxxxxxxxxxxxxxxxxxx  私钥: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

![](./collider.png)

Telegram: https://t.me/laomaok

weixin: laomao12a

### 波场靓号生成器程序
<a href="https://github.com/jeffcail/batch_generate_tron_address" target="_blank">波场靓号生成器程序</a>

### 波场钱包源码
<a href="https://github.com/jeffcail/tron-wallet" target="_blank">波场钱包源码</a>
