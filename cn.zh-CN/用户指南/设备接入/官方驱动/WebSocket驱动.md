# WebSocket驱动 {#concept_745040 .concept}

Link IoT Edge提供用于接入WebSocket通信协议设备的驱动。根据网关设备使用架构的不同，Link IoT Edge提供多种WebSocket驱动。您可以直接从控制台部署WebSocket驱动到网关。

使用WebSocket驱动接入设备时需要遵循Link IoT Egde的WebSocket接入协议。详情请参见[物联网边缘计算设备接入协议（WebSocket版）](https://github.com/aliyun/linkedge-thing-access-websocket_client_sdk/blob/master/protocol.md)。

WebSocket驱动可以直接接受设备的接入，示意图如下所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/602307/156222346949749_zh-CN.png)

WebSocket驱动也可以通过网关接受设备的接入，示意图如下所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/602307/156222346950381_zh-CN.png)

## 使用步骤 {#section_2kn_rjj_bk9 .section}

1.  参考[环境搭建](cn.zh-CN/用户指南/环境搭建/专业版环境搭建/基于Ubuntu 16.04搭建环境.md#)，创建边缘实例并上线网关。
2.  在**边缘计算** \> **边缘实例**页面，选择已创建的边缘实例，单击右侧的**查看**。
3.  在**实例详情**页面，选择设备驱动配置，单击**全部驱动**右侧的“`+`”图标 。
4.  在分配驱动弹出窗口中，根据网关CPU架构选择需要使用的WebSocket驱动，单击对应操作栏中的**分配**。然后单击**完成**。

    **说明：** WebSocket驱动，仅支持在v1.8.4及以上版本的Link IoT Edge中使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/602307/156222347049844_zh-CN.png)

5.  单击已分配的WebSocket驱动，在设备列表右侧单击**驱动配置**。

    根据界面提示设置参数，然后单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/602307/156222347049853_zh-CN.png)

    |参数|描述|
    |--|--|
    |IP地址|WebSocket驱动监听地址，默认为驱动所在本机地址。|
    |端口号|WebSocket驱动监听端口，范围为1 ~ 65535，默认端口为17682。|
    |是否加密|是否使用TLS加密，默认不加密。若选择**是**，需要上传公钥和私钥文件。     -   公钥文件：上传公钥证书文件，证书文件格式必须为.cer，名称不支持中文字符。
    -   私钥文件：上传私钥文件，文件格式必须为.pvk，名称不支持中文字符。
 |

6.  （可选）在设备列表右侧，单击**容器配置**，可参考[容器配置](https://help.aliyun.com/document_detail/85162.html#title-9kr-v8d-aj1)中的参数说明，对当前驱动进行容器配置。配置完成后单击**确定**。

    **说明：** 仅在产品规格为专业版的边缘实例中，允许设置**容器配置**。

7.  单击**分配子设备**，在WebSocket驱动下为边缘实例分配设备。

    您可以分配已有的WebSocket设备，也可以根据如下步骤，新建WebSocket设备。

    1.  在右侧弹出的分配子设备页面中，单击**添加子设备**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/117119/156222347037903_zh-CN.png)

    2.  在添加设备页面，单击**新建产品**，创建WebSocket设备所属产品。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/117119/156222347037904_zh-CN.png)

    3.  在创建产品页面设置参数后，单击**确认**。

        |参数|描述|
        |--|--|
        |产品名称|设置产品名称，产品名称在账号内具有唯一性。|
        |所属分类|选择品类，为该产品定义[物模型](cn.zh-CN/用户指南/产品与设备/物模型/概述.md#)。此处选择自定义品类。|
        |接入网关协议|此处必须选择自定义。|

    4.  在添加设备页面，输入设备名称，添加WebSocket设备。
    5.  将新建的WebSocket设备**分配**到边缘实例。
8.  分配设备到边缘实例后，单击设备名称对应操作栏中的**设备配置**，关联设备与WebSocket驱动。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/602307/156222347050342_zh-CN.png)

    设备IP：接入设备或设备所在网关的IP。

    **说明：** 如果配置设备IP，则严格校验IP，仅允许符合该IP、所属产品名、Devicename的设备接入。

    至此，您已完成WebSocket驱动的分配。

9.  （可选）如果需要将设备数据上报到云端，则需要配置消息路由，详情请参见[设置消息路由](cn.zh-CN/用户指南/消息路由/设置消息路由.md#)。
10. 在实例详情页面，单击界面右上角**部署**，重新部署边缘实例。

