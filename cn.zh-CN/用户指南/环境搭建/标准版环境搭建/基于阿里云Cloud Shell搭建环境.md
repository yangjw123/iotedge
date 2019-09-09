# 基于阿里云Cloud Shell搭建环境 {#task_1495784 .task}

本文介绍基于阿里云云命令行（Cloud Shell），快速将网关连接到物联网边缘计算控制台，并将网关数据上传至云端。Cloud Shell是阿里云提供的网页版命令行工具。您可以在任意浏览器上运行云命令行管理阿里云资源。

然而在Cloud Shell中操作时，若连续15分钟不做任何操作，系统会自动退出，并清空您保存在Cloud Shell上的资料，因此不建议您使用Cloud Shell作为开发生产环境，仅用于快速了解并无任何门槛地使用Link IoT Edge。在开始操作本章内容前，请您仔细阅读[Cloud Shell介绍及使用限制](https://help.aliyun.com/document_detail/90256.html)。

Cloud Shell仅支持搭建v1.8.2及以上版本的Link IoT Edge标准版（LE Standard）软件包。

## 创建边缘实例和网关 {#section_e7q_nbs_e0t .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。 
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。 物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717637158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。 物联网边缘计算中的新建网关产品继承物联网平台 **设备管理** \> **产品**中的产品功能，已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![创建产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717637159_zh-CN.png)

        |参数|说明|
        |--|--|
        |产品名称|为网关产品设置名称，用于后续的查询及识别网关产品。支持中文、英文字母、数字和下划线，长度限制4~30，一个中文汉字算2位。|
        |所属分类|选择品类，为该产品定义[物模型](../cn.zh-CN/用户指南/产品与设备/物模型/什么是物模型.md#)。 可选择为：

         -   **自定义品类**：需根据实际需要，定义产品功能。
        -   任一既有功能模板。

选择任一物联网平台预定义的品类，快速完成产品的功能定义。选择产品模板后，您可以在该模板基础上，编辑、修改、新增功能。

 若您需要的网关没有特殊功能定义，建议您选择**自定义品类**。

 |
        |产品描述|可输入文字，用来描述产品信息。字数限制为100。可以为空。|

        产品创建成功后，页面自动跳转回新增实例页面，并且**网关产品**参数下自动分配了刚创建的网关产品。

    4.  在新增实例页面，单击**网关设备**后的**新建网关设备**为网关产品添加设备。 物联网边缘计算中的新建网关设备功能继承物联网平台 **设备管理** \> **设备**的功能。

        ![新建网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717637160_zh-CN.png)

    5.  根据界面提示设置参数后，单击**确认**。 

        |参数|描述|
        |--|--|
        |产品|系统已自动关联上一步创建的网关产品。|
        |设备名称|为该网关设备命名。设备名称需保持产品内唯一。如不填写，系统将自动生成。 **说明：** 设备名称支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

 |

    6.  根据所搭建的环境，选择对应的Link IoT Edge产品规格，详细介绍请参见[产品规格](../cn.zh-CN/产品简介/产品规格.md#)。
    7.  （可选）在新增实例页面，单击**新增标签**，可以设置实例标签。通过标签您可以更加有效地归类及识别实例。您也可以不设置标签。
3.  实例参数设置完成后，单击**确定**，至此您已创建边缘实例和网关。

## 启动Link IoT Edge {#section_n2l_4ax_8u0 .section}

1.  在左侧导航栏中选择**边缘计算** \> **边缘实例**，单击实例名称右侧的**软件安装**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717644201_zh-CN.png)

2.  根据环境设置下载参数，然后单击**生成安装命令**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156801717644200_zh-CN.png)

    |参数|描述|
    |--|--|
    |CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](../cn.zh-CN/产品简介/发布历史/专业版.md#)。|
    |操作系统|选择您的设备对应的操作系统。此处选择CloudShell。|

    如果您暂时没有合适的硬件载体来运行Link IoT Edge，您可以单击对话框上方的**立即体验**，使用Cloud Shell虚拟机快速体验标准版Link IoT Edge的产品功能。使用**立即体验**功能有诸多注意事项，详情请参见[使用体验版本Link IoT Edge（可选）](cn.zh-CN/用户指南/环境搭建/标准版环境搭建/基于Ubuntu 16.04搭建环境.md#section_vm1_jws_lzz)。

3.  复制操作系统命令备用。 

    ![复制命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156801717644205_zh-CN.png)

4.  以阿里云账号登录 [Cloud Shell](https://shell.aliyun.com/)。
5.  在授权提示窗口中，单击**确认**授权Cloud Shell获取临时的会话访问密钥。 

    ![授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135995/156801717740466_zh-CN.png)

6.  在挂载存储空间提示窗口中，选择**暂不创建**。 

    ![挂载存储空间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135995/156801717740467_zh-CN.png)

    等待15 ~ 30秒后系统成功登录Cloud Shell，操作界面如下图所示。

    ![cloudsell操作界面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135995/156801717740399_zh-CN.png)

7.  任意目录下执行步骤3中已复制的命令。 该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge-standard.sh脚本。

    **说明：** 如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge-standard.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图：

    ![其他操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717744213_zh-CN.png)

8.  执行如下命令查看Link IoT Edge核心服务的运行状态。 

    ``` {#codeblock_ach_dv9_fte}
    ./iot_gateway_status.sh
    ```

    若系统显示如下信息，表示Link IoT Edge核心服务启动成功。

    ![LE启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135995/156801717740402_zh-CN.png)

    您也可以在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例** ，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/103167/156801717748660_zh-CN.png)

9.  （可选）在实例详情页面，查看CPU使用率、内存使用率、存储使用率以及实例进程需要授权访问阿里云云监控（CloudMonitor）服务。 
    1.  请根据[云资源访问](../cn.zh-CN/用户指南/云资源访问.md#)内容，添加角色或分配已有的角色，并为该角色添加**管理云监控（CloudMonitor）的权限**。
    2.  选择**设置**页签，在实例信息中打开**云监控状态**按钮，如下图所示。 

        ![打开云监控](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156801717737199_zh-CN.png)

        云监控状态打开后，可在实例详情页面选择**监控信息**，查看网关的各类监控信息。


## 下一步 {#section_ufa_drh_uyh .section}

环境搭建完成后，您可以根据[设备接入](../cn.zh-CN/用户指南/设备接入/设备接入简介.md#)章节内容，把您的设备接入到物联网边缘计算。同时也可以为边缘实例分配其他资源（如函数计算、消息路由等）管理您的设备。

接入设备或分配其他资源到边缘实例后，需要根据如下步骤部署边缘实例。

1.  在实例详情页面，单击右上角**部署**后在弹出框中单击**确定**，部署边缘实例。
2.  当部署状态显示为**部署成功**，表示部署实例完成。您可以单击**查看日志**，查看部署详情。 

    ![查看部署日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/301656/156801717848671_zh-CN.png)


