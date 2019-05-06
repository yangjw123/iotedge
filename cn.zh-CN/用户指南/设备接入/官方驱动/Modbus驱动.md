# Modbus驱动 {#concept_ytg_13d_x2b .concept}

Link IoT Edge提供Modbus和OPC UA两种官方驱动，用于支持设备使用Modbus和OPC UA这两种工业领域应用广泛的通信协议。本文主要介绍Modbus驱动及其用法。

Modbus是常用的应用层数据通信协议，阿里云官方Modbus驱动（以下简称Modbus驱动）支持Modbus-RTU和Modbus-TCP两种交互。

Modbus驱动可以直接连接Modbus从设备，详情见下图。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18136/155713287639309_zh-CN.png)

Modbus驱动也可以通过Modbus网关连接Modbus从设备，详情见下图。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18136/155713287639310_zh-CN.png)

Modbus驱动支持的功能有读取输入状态和输入寄存器，读/写线圈状态和保持寄存器。

根据设备使用的语言和架构的不同，Link IoT Edge提供多种Modbus驱动。您可以直接从控制台部署Modbus驱动到网关，也可以从控制台下载Modbus驱动代码进行修改，作为您的自定义驱动使用。

Modbus驱动使用步骤如下：

1.  [搭建边缘环境](cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md#)。
2.  创建产品，并选择接入网关协议为Modbus，具体创建产品步骤请参见[创建产品](../../../../cn.zh-CN/用户指南/产品与设备/创建产品.md#)。
3.  为产品添加设备，具体添加设备步骤请参见[单个创建设备](../../../../cn.zh-CN/用户指南/产品与设备/创建设备/单个创建设备.md#)和[批量创建设备](../../../../cn.zh-CN/用户指南/产品与设备/创建设备/批量创建设备.md#)。
4.  为产品定义物模型，具体定义方法请参见[新增物模型](../../../../cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md#)。
5.  完成上述设备配置后，需要配置设备与网关的交互方式。
    1.  创建子设备通道，具体方法请参见[子设备通信通道](cn.zh-CN/用户指南/设备接入/子设备通信通道.md#)。
    2.  将设备分配到边缘实例，作为网关子设备后，为子设备配置Modbus驱动，关联子设备通信通道。
6.  重新部署边缘实例。

