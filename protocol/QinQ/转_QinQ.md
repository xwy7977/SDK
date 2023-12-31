[原文地址：https://info.support.huawei.com/info-finder/encyclopedia/zh/QinQ.html](https://info.support.huawei.com/info-finder/encyclopedia/zh/QinQ.html)

# QinQ

## 什么是QinQ

QinQ（802.1Q-in-802.1Q），也叫做VLAN Stacking或Double VLAN，由IEEE 802.1ad标准定义，是一项扩展VLAN空间的技术，通过在802.1Q标签报文的基础上再增加一层802.1Q的Tag来达到扩展VLAN空间的目的。一般应用在骨干网中，通过将用户私网VLAN Tag封装在公网VLAN Tag中，使报文带着两层VLAN Tag穿越运营商的骨干网络（公网），扩充VLAN数量，实现对用户的精细化管理。

## 为什么需要QinQ

IEEE 802.1Q中定义的VLAN ID只有12个比特，仅能表示4096个VLAN域，随着网络规模的扩大，4096个VLAN域已无法满足网络扩容的需求，为此，IEEE 802.1ad中在原有的802.1Q报文的基础上增加一层802.1Q Tag（也叫做VLAN Tag或标签），使VLAN数量增加到4094×4094，这种双层Tag的报文就叫做QinQ报文。

随着以太网的进一步发展以及运营商精细化运作的要求，QinQ的双层Tag又有了新的应用场景。它的内外层Tag可以代表不同的信息，如内层Tag代表用户，外层Tag代表业务。另外，QinQ报文带着两层Tag穿越运营商网络，内层Tag透明传送，也是一种简单、实用的VPN技术。

所以，QinQ产生的两大背景是：一是解决日益紧缺的VLAN ID资源问题；二是满足业务精细化管理的需求。

## QinQ应用场景有哪些

在企业网中，可以不同的业务封装不同VLAN Tag，使不同的业务按需获取不同的资源。如下图所示，PC、VOIP、IPTV由于应用场景和需求不同，在企业内部属于不同的VLAN，访问公网时，针对不同的内层VLAN Tag添加不同的外层VLAN Tag。

* PC：内层VLAN Tag对应的VLAN ID是101，外层VLAN Tag对应的VLAN ID是1001
* VOIP：内层VLAN Tag对应的VLAN ID是301，外层VLAN Tag对应的VLAN ID是2001
* IPTV：内层VLAN Tag对应的VLAN ID是501，外层VLAN Tag对应的VLAN ID是3001

![QinQ_1](./转_QinQ.assets/QinQ_1.png)

在运营商网络中，为节省运营商公网VLAN ID资源，用户在使用运营商网络传输报文时，内层使用不同的VLAN ID区分不同部门，外层使用相同的VLAN ID。如下图所示，不同区域部门的用户需要跨越运营商网络相互通信，为节省运营商VLAN ID，用户报文在运营商网络中转发时，统一都添加一层VLAN ID为3的Tag。

![QinQ_2](./转_QinQ.assets/QinQ_2.png)

## QinQ报文格式

QinQ报文有固定的格式，就是在802.1Q的标签之上再打一层802.1Q标签，QinQ报文比802.1Q报文多四个字节。这四个字节用作外层标签，即运营商网络的公网VLAN Tag。原802.1Q的Tag用作内层标签，即私网VLAN Tag。QinQ报文封装格式如下图所示。

![QinQ_3](./转_QinQ.assets/QinQ_3.png)

如下图所示，通过对802.1Q封装和QinQ封装的报文抓包，可以明显看出QinQ报文比802.1Q多了一层802.1Q标签。

![QinQ_4](./转_QinQ.assets/QinQ_4.png)

## QinQ有哪些实现方式

根据识别报文的方式和添加外层标签的位置，QinQ的实现方式可以分为下面两种。

* 基于接口的QinQ封装：也叫做基本QinQ或QinQ隧道（QinQ Tunnel），就是对接口收到的所有报文都添加一层VLAN ID相同的外层Tag。
* 基于流的QinQ封装：也叫做灵活QinQ，首先对进入接口的报文根据指定规则分类，然后对于不同类型的报文选择封装何种外层Tag。例如：当同一企业的不同业务使用不同的VLAN ID时，可以根据VLAN ID进行对报文进行分类。假设PC上网的VLAN ID范围是101～200；IPTV的VLAN ID范围是201～300；大客户的VLAN ID范围是301～400。设备收到业务报文后，可以根据VLAN ID范围对不同的业务添加不同的外层Tag。对PC上网业务封装上外层Tag 100，对IPTV封装上外层Tag 300，对大客户封装上外层Tag 500。

常见的对报文分类的方式包括如下几种：
* 根据报文原有的VLAN ID进行分类，即根据报文原有内层VLAN ID添加不同的外层VLAN Tag。
* 根据报文原有的VLAN Tag中的802.1p优先级进行分类，即根据报文原有内层VLAN的802.1p优先级添加不同的外层VLAN Tag。
* 根据流策略进行精细分类，即根据QoS策略添加不同的外层VLAN Tag。该方式能够针对业务类型提供差别服务。

## QinQ是如何工作的

在QinQ典型组网中，有两个重要的设备角色：CE（Customer Edge）设备和PE（Provider Edge ）设备。CE设备与用户相连，对用户报文封装第一层VLAN Tag，即内层VLAN Tag；PE设备是CE设备的下游设备，对CE设备转发过来的报文封装第二层VLAN Tag，即外层VLAN Tag。

如下图所示，部门A和部门B分布在不同的办公点，部门A和部门B通过运营商网络相互通信，部门A和部门B分别使用VLAN 10和VLAN 20进行通信，该企业仅申请到一个公网VLAN 3。当CE1和CE3对应的部门A的用户相互通信时，CE1用户发送到CE3用户的报文，VLAN Tag的添加和剥离流程如下。

1. CE1收到用户报文时，对用户报文封装第一层VLAN Tag，对应的VLAN ID是10。
2. PE1收到CE1转发的用户报文时，对用户报文再封装一层VLAN Tag，对应的VLAN ID是3。
3. 报文携带两层VLAN Tag（内层VLAN Tag的VLAN ID是10，外层VLAN Tag的VLAN ID是3），从PE1设备传输到PE2设备。
4. PE2收到报文从对应出接口转发报文时，会剥离掉外层VLAN ID是3的VLAN Tag。
5. CE3收到报文时，报文仅携带一层VLAN ID为10的VLAN Tag。CE3设备转发报文时，会剥离掉这层VLAN ID为10的 VLAN Tag。

CE3用户发送到CE1用户的报文，VLAN Tag的添加和剥离流程正好与上面流程相反。

![QinQ_5](./转_QinQ.assets/QinQ_5.png)

## QinQ相关技术

### VLAN Mapping

如上描述，通过QinQ技术可以实现两个VLAN相同的二层用户网络通过骨干网络互联，但是通过QinQ技术需要增加额外的报文开销（增加一层VLAN Tag）。通过VLAN Mapping技术也可以实现两个VLAN相同的二层用户网络通过骨干网络互联。

一侧用户网络的带有VLAN Tag的二层报文进入骨干网后，骨干网边缘设备将用户网络的VLAN（称为C-VLAN）修改为骨干网中可以识别和承载的VLAN（称为S-VLAN），传输到另一侧之后，边缘设备再将S-VLAN修改为C-VLAN。这样就可以很好的实现两个用户网络二层无缝连接。

VLAN Mapping还可以应用在另一种场景中，如果由于规划的差异，导致两个直接相连的二层网络中部署的VLAN ID不一致。但是用户又希望可以把两个网络作为单个二层网络进行统一管理。此时也可以在连接两个网络的交换机上部署VLAN Mapping功能，实现两个网络之间不同VLAN ID的映射，达到二层互通和统一管理的目的。

### VXLAN

VXLAN（Virtual eXtensible Local Area Network），也称为虚拟可扩展LAN，顾名思义，VXLAN是一种扩展VLAN的网络虚拟技术。VXLAN作为NVO3技术之一，本质上也属于一种VPN技术，能够在任意路由可达的网络上叠加二层虚拟网络，通过VXLAN网关实现VXLAN网络内部的互通，同时，也可以实现与传统的非VXLAN网络的互通。另外，VXLAN通过引入了类似VLAN ID的用户标识，VXLAN网络标识VNI（VXLAN Network Identifier），由24比特组成，支持多达16M的VXLAN段，解决云计算中海量租户隔离的问题。