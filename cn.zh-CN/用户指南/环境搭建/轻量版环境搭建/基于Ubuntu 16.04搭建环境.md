# 基于Ubuntu 16.04搭建环境 {#task_1495784 .task}

本文介绍基于Ubuntu 16.04系统搭建Link IoT Edge轻量版本（LE Lite）运行环境的方法。

-   Link IoT Edge的远程登录功能依赖设备的SSH服务，请确保设备上已经开启了SSH服务。SSH的详细信息可参考[OpenSSH的使用](https://help.ubuntu.com/lts/serverguide/openssh-server.html.en?spm=a2c4g.11186623.2.11.3ce2427aDPqjvW&file=openssh-server.html.en)。
-   请确保设备的本地环回端口已启用，即在设备上执行ping 127.0.0.1命令时，返回结果正常。

## 创建边缘实例和网关 {#section_e7q_nbs_e0t .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。 
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。 物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618495537158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。 物联网边缘计算中的新建网关产品继承物联网平台 **设备管理** \> **产品**中的产品功能，已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![创建产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618495537159_zh-CN.png)

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

        ![新建网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618495537160_zh-CN.png)

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

1.  在左侧导航栏中选择**边缘计算** \> **边缘实例**，单击实例名称右侧的**下载**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618495544201_zh-CN.png)

2.  根据环境设置下载参数，然后单击**生成命令**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618495544238_zh-CN.png)

    |参数|描述|
    |--|--|
    |CPU架构|您的设备系统对应的CPU架构。此处选择x86-64。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](../cn.zh-CN/产品简介/发布历史/专业版.md#)。|
    |操作系统|选择您的设备对应的操作系统。此处选择Linux|

3.  复制操作系统命令备用。 

    ![复制命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618495644857_zh-CN.png)

4.  登录您Ubuntu 16.04系统的机器。
5.  任意目录下执行步骤3中已复制的命令。 该命令实现一键下载、配置并启动Link IoT Edge。命令执行完成后，会在当前目录中下载link-iot-edge-lite.sh脚本。

    **说明：** 如果不是第一次安装启动Link IoT Edge，可使用已下载的link-iot-edge-lite.sh脚本，对Link IoT Edge进行重启、停止、获取状态、修改配置参数等操作，命令详情请见下图：

    ![轻量版操作命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618495644855_zh-CN.png)

    若系统显示如下信息，表示Link IoT Edge核心服务启动成功。

    ![LE启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618495637295_zh-CN.png)

    您也可以在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例** ，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618495748694_zh-CN.png)


## 使用systemd管理Link IoT Edge {#section_0iy_5o0_06a .section}

-   下载service文件。

    ``` {#codeblock_s96_ubn_ytq}
    wget http://remote-access-oxs.oss-cn-shanghai.aliyuncs.com/%E8%84%9A%E6%9C%AC/LinkIoTEdgeLite.service
    ```

-   将service文件拷贝到/etc目录。

    ``` {#codeblock_8nx_x2h_evp}
    sudo cp LinkIoTEdgeLite.service /etc/systemd/system/LinkIoTEdgeLite.service
    ```

-   启动Link IoT Edge。

    ``` {#codeblock_hr0_o0j_8d2}
    sudo systemctl start LinkIoTEdgeLite.service
    ```

-   停止Link IoT Edge。

    ``` {#codeblock_jtn_8do_cba}
    sudo systemctl restart LinkIoTEdgeLite.service
    ```

-   开机自启动Link IoT Edge。

    ``` {#codeblock_h86_hqo_4ez}
    sudo systemctl enable LinkIoTEdgeLite.service
    ```


## 下一步 {#section_zgy_dbs_lwl .section}

1.  **实例详情**页面选择**设置**页签，并在实例信息下，打开远程调试后的按钮。
2.  **实例详情**页面选择**网关**页签，在网关名称右侧的操作栏中单击**远程连接**、**远程文件管理**或者**更多远程服务**，远程控制网关设备或对网关设备上的文件进行管理。详细说明请参见[远程服务访问](../cn.zh-CN/用户指南/远程运维管理/远程服务访问.md#)。

