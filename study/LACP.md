# LACP链路聚合控制协议

参考：[LACP] (https://www.cnblogs.com/taosim/articles/4378691.html)

在过去的10年里，以太网线速(Line Rate)的发展从10Mb/s -> 100Mb/s -> 1Gb/s -> 10Gb/s(40GE和100GE也已出现)，而然有的时候single 10GE link依然无法满足VLAN Trunk或iSCSI/FCoE流量对带宽和冗余性的需求。于是链路聚合(Link Aggregation，LA)技术出现了，这是一种将多个网络链路合并成单条逻辑链路，从而提供更大带宽和冗余的网络技术。

注：本文多次用到Link Aggregation、Port Aggregation、Port Channel、Link Channel等术语，如未特别指出，可认为是同一个意思。

## Link Aggregation

 不同厂商交换机的端口聚合(Port Aggregation，PA)采用不同术语，Cisco的EtherChannel，Brocade的Brocade LAG，还有基于标准的IEEE 802.3ad LACP(Link Aggregation Control Protocol，该标准在2008年被转入IEEE 802.1ax)，LACP可以动态配置端口聚合，且不依赖任何厂商，因此大部分以太网交换机都支持该协议。所有这些实现的目标都是一致的，即将两个或多个端口绑定在一起作为一个高带宽的逻辑端口来提升链路速度、冗余、弹性和负载均衡。技术上来讲，我们可以在交换机之间使用多个端口创建并行trunk链路，但生成树协议(STP)将其视为环路，从而会关闭所有可能造成环路的链接。端口聚合生成single logical link，不会造成环路，可作为Access Port(连接主机)或Trunk Port(承载Multi-VLAN traffic)使用。

 - 在使用LA技术之前，有必要了解如下技术属性：

 - 兼容性/正常运行：聚合链路每一端的交换机或主机必须理解或使用公共的端口聚合技术

 - 负载均衡：通过哈希算法在single link中区分不同的traffic pattern来实现

 - 链路冗余：如果逻辑链路中的一条物理链路故障，流量转走临近的链路，故障转移时间一般小于几个毫秒。一旦失败链路恢复，流量会重新分布。

 在选择端口做端口聚合或端口隧道(port channel)时，每个端口需要互相兼容，可以在允许将端口加入端口聚合组(Port Channel Group)之前，检查端口的运行属性，兼容性检查通常包括以下接口运行属性：

 - Port Mode

 - Access VLAN

 - Trunk native VLAN
 
 - 允许的VLAN列表

 - Speed