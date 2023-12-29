# 慢协议（slow protocol）

## 概述

有两类不同的协议用于控制IEEE 802.3设备的运行：

- 需要快速处理和响应PDU以避免性能下降的协议，如 MAC Control PAUSE operation（附件31B）。这些协议可能在嵌入式硬件中实现，所以现有设备不太可能轻易的增加对此类协议的支持，除非升级设备。

- 频率和延迟要求不那么严格的协议，比如LACP。这些协议可以在软件中实现，现有的设备也可以通过升级软件来支持此类协议。

## 慢协议传输特性

IEEE 802.3 标准中的慢协议具有以下限制：

- 每秒钟传输的帧的数量应该小于等于 aSlowProtocolFrameLimit （默认值是10）。

- 慢协议子类型的最大数量是10。

- 这些协议生成的MAC Client数据不应该超过maxBasicDataSize（1500），推荐慢协议帧的大小最大为128字节（OAMPDU是超过128字节的）。

## 慢协议多播地址

慢协议PDU使用专门分配给他的多播地址（Slow_Protocols_Multicast address），是`01-80-C2-00-00-02`。已经存在的慢协议（比如LACP和Marker）是使用这个MAC地址的，但是将来的新的慢协议并不一定会使用。

## 慢协议标识

所有的慢协议都使用长度/类型（Length/Type）字段进行标识，慢协议该字段的值是`8809`。

紧跟着长度/类型（Length/Type）字段的是协议的子类型标识符，以区分不同的慢协议。目前，子类型的值有如下几种：

- 1  <--> Link Aggregation Control Protocol (LACP)
- 2  <--> Link Aggregation—Marker Protocol
- 3  <--> Operations, Administration, and Maintenance (OAM)
- 10 <--> Organization Specific Slow Protcol (OSSP)

## 对慢协议帧的处理

任何接收到的携带 Slow_Protocols_Type 字段值（8809）的 MAC 帧都被假定为慢协议帧。应按如下方式处理所有慢协议帧：

- 如果慢协议帧携带了非法子类型（子类型为  0 或 11-255），此类帧不得传递至 MAC Client,直接丢弃。
- 如果慢协议帧的子类型符合要求（即属于上文中的某一种，子类型为1,2,3,10），将此类帧传给对应的协议实体。
- 其他的慢协议帧传递给MAC Client。

## 参考

[802.3-2018 - IEEE Standard for Ethernet | IEEE Standard | IEEE Xplore](https://ieeexplore.ieee.org/document/8457469)

[8023-57a_b_SG15CMP.fm](https://www.ieee802.org/3/axay/comments/D1.2/8023-57a_b_SG15CMP_response.pdf)

[What is Slow Protocols / Sudo Null IT News](https://sudonull.com/post/126874-What-is-Slow-Protocols)

[What is Slow Protocol | SEの道標](https://milestone-of-se.nesuke.com/en/nw-basic/link-aggregation/slow-protocol/)

[学习笔记——Slow Protocol，慢协议_slow-protocols-CSDN博客](https://blog.csdn.net/dandandean_96/article/details/81530801)