# OPC UA驱动 {#concept_221130 .concept}

Link IoT Edge产品提供用于接入OPC UA设备的驱动（简称OPC UA驱动）。您可以直接从控制台部署OPC UA驱动到网关，也可以从控制台下载OPC UA驱动代码进行修改，作为您的自定义驱动使用。

OPC UA驱动目前仅支持在Link IoT Edge专业版（LE Pro）上运行。

## 概述 {#section_rsf_b40_ex0 .section}

OPC UA驱动和OPC UA设备的连接是通过OPC UA服务器关联的，OPC UA驱动通过操作OPC UA服务器对外暴露的协议接口操作OPC UA设备，详情见下图。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18136/156222339933401_zh-CN.png)

## 使用步骤 {#section_i5o_ekj_lg3 .section}

OPC UA驱动的使用步骤如下：

**说明：** 详细的OPC UA驱动使用示例，请参见[OPC UA设备接入实践](../../../../cn.zh-CN/最佳实践/OPC UA设备接入实践.md#)。

1.  参考[环境搭建](cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md#)，创建边缘实例并上线网关。
2.  在**边缘计算** \> **边缘实例**页面，选择已创建的边缘实例，单击右侧的**查看**。
3.  在**实例详情**页面，选择设备驱动配置，单击**全部驱动**右侧的“`+`”图标 。
4.  在分配驱动弹出窗口中，选择OPC UA驱动，单击对应操作栏中的**分配**。然后单击**完成**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/188524/156222339948705_zh-CN.png)

5.  单击已分配的OPC UA驱动，在设备列表右侧单击**驱动配置**。
6.  在弹出窗口中单击**添加通道**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/188524/156222339950545_zh-CN.png)

7.  根据界面提示设置参数，然后单击**确定**。

    |参数|描述|
    |:-|:-|
    |通道名称|需在网关维度具有唯一性。|
    |通道地址|如`opc.tcp://localhost:4840`。|
    |安全策略|指加密算法策略。有NoneBasic128Rsa15、Basic256三种。|
    |安全模式|指签名类型。有NoneSign、SignAndEncrypt三种。|
    |用户名|非必填。|
    |密码|非必填。|
    |方法调用超时时间|单位为秒。|

8.  （可选）在设备列表右侧，单击**容器配置**，可参考[容器配置](https://help.aliyun.com/document_detail/85162.html#title-9kr-v8d-aj1)中的参数说明，对当前驱动进行容器配置。配置完成后单击**确定**。

    **说明：** 仅在产品规格为专业版的边缘实例中，允许设置**容器配置**。

9.  单击**分配子设备**，在OPC UA驱动下为边缘实例分配设备。
    -   可以分配已在物联网平台创建的OPC UA设备（详细说明请参见[创建产品](../../../../cn.zh-CN/用户指南/产品与设备/创建产品.md#)，该设备所属产品必须接入网关，且接入网关协议为OPC UA。
    -   也可以根据如下步骤，新建OPC UA设备。
    1.  在右侧弹出的分配子设备页面中，单击**添加子设备**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/117119/156222339937903_zh-CN.png)

    2.  在添加设备页面，单击**新建产品**，创建OPC UA设备所属产品。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/117119/156222339937904_zh-CN.png)

    3.  在创建产品页面设置参数后，单击**确认**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/188524/156222340048787_zh-CN.png)

        |参数|描述|
        |--|--|
        |产品名称|设置产品名称，产品名称在账号内具有唯一性。|
        |所属分类|选择品类，为该产品定义[物模型](cn.zh-CN/用户指南/产品与设备/物模型/概述.md#)。此处选择自定义品类。|
        |接入网关协议|此处必须选择OPC UA。|

    4.  返回添加设备页面，添加OPC UA设备。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/188524/156222340048788_zh-CN.png)

    5.  在分配子设备页面，将新建的OPC UA设备分配到边缘实例。
10. 分配设备到边缘实例后，单击设备名称对应操作栏中的**设备配置**，通过关联通道，关联设备与OPC UA驱动。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/188524/156222340048789_zh-CN.png)

    |参数|描述|
    |--|--|
    |关联通道|选择本文上方步骤6中已创建的通道。|
    |节点路径|设备在OPC UA Server中，从Objects开始到设备节点的绝对路径。 **说明：** OPC UA Server相关说明请参见[OPC UA设备接入实践](../../../../cn.zh-CN/最佳实践/OPC UA设备接入实践.md#)。

 |

    至此，您已完成OPC UA驱动的分配。

11. （可选）如果需要将设备数据展示在云端，则需要配置消息路由，详情请参见[设置消息路由](cn.zh-CN/用户指南/消息路由/设置消息路由.md#)。
12. 在实例详情页面，单击右上角**部署**，重新部署边缘实例。

