# 使用Modbus TCP连接Modbus从设备 {#concept_z5s_gkc_ggb .concept}

Modbus通信协议遵循主设备和从设备的通信步骤，边缘网关中Modbus驱动使用Master角色采取主动询问方式，送出Query Message给Modbus从设备，然后由Modbus从设备依据接到的Query Message内容准备Response Message回传给网关。

## 前提条件 {#section_yw1_gsd_ggb .section}

1.  准备一个Ubuntu 16.04 x86\_64系统，用于运行网关。
2.  准备一个Windows系统的机器，用于运行模拟的Modbus从设备。
3.  从[这里](https://www.modbustools.com/download.html)获取Modbus从设备模拟软件，并下载到Windows机器上。
4.  检查Windows机器的防火墙，确保能正常访问Modbus从设备502端口，若不能访问，请关闭防火墙或者防火墙中允许访问端口。

## 操作步骤 {#section_zv4_gsd_ggb .section}

1.  以阿里云账号登录[物联网控制台](http://iot.console.aliyun.com/)。
2.  参考[环境搭建](../../../../cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md#)内容，创建边缘实例，上线网关。
3.  参考[Modbus驱动](../../../../cn.zh-CN/用户指南/设备接入/官方驱动/Modbus驱动.md#)中的使用步骤，根据网关CPU，分配适合的Modbus驱动到边缘实例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666746392_zh-CN.png)

4.  单击已分配的Modbus驱动，在设备列表右侧单击**驱动配置**。
5.  在弹出窗口中单击**添加通道**，为Modbus驱动添加通道。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666735187_zh-CN.png)

6.  参考[Modbus驱动](../../../../cn.zh-CN/用户指南/设备接入/官方驱动/Modbus驱动.md#)中的使用步骤，创建Modbus产品。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666849165_zh-CN.png)

7.  设置创建产品的参数。

    其中，部分参数必须按如下说明设置。

    |参数|描述|
    |--|--|
    |所属分类|选择**自定义分类**。|
    |接入网关协议|选择**Modbus**。|

8.  在添加设备页面，产品自动分配已创建的产品，单击产品下的**前往设置**，为产品添加自定义功能。
9.  参考[新增物模型](../../../../cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md#)中的自定义功能，设置参数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666835180_zh-CN.png)

10. 单击**扩展描述**。

    通过新增扩展描述对Modbus的点位进行描述。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666835181_zh-CN.png)

    对Modbus点位描述时需要参考模拟的Modbus从设备中的点位设置，如下图所示。本文示例产品中创建了3个属性点aaa、bbb、ccc分别对应Modbus从设备中点位地址0，1，2三个地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666935182_zh-CN.png)

11. 返回实例详情页面，添加Modbus设备。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666935186_zh-CN.png)

12. 将新建的Modbus设备分配到边缘实例，并进行**设备配置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666949270_zh-CN.png)

    部分参数说明如下：

    |参数|描述|
    |--|--|
    |关联通道|选择已在第5步中添加的通道。|
    |从站号|从站号参考第10步中点位的ID值，即本示例中从站号为1。|

13. 配置并部署边缘实例。
    1.  在分配子设备页面，将已创建的Modbus设备**分配**到边缘实例中。
    2.  配置如下图消息路由。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047666935188_zh-CN.png)

    3.  部署边缘实例。
14. 在**设备管理** \> **设备**页，运行状态页签中，查看设备显示的属性。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83053/156047667035189_zh-CN.png)


