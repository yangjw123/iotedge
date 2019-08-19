# 基于MacOS搭建环境 {#task_1495784 .task}

本文介绍如何在MacOS系统中搭建Link IoT Edge轻量版（LE Lite）运行环境。

MacOS设备需要预先配置远程桌面服务，否则无法远程访问。MacOS下SSH服务开启方法如下。

1.  登录MacOS系统设备。
2.  打开**系统偏好设置** \> **共享**。
3.  勾选**远程登录**。

    ![远程登录](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149667/156618511441582_zh-CN.png)


## 创建边缘实例和网关 {#section_lfh_y3b_08w .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。 
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。 物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618511537158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。 物联网边缘计算中的新建网关产品继承物联网平台 **设备管理** \> **产品**中的产品功能，已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![创建产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618511537159_zh-CN.png)

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

        ![新建网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618511537160_zh-CN.png)

    5.  根据界面提示设置参数后，单击**确认**。 

        |参数|描述|
        |--|--|
        |产品|系统已自动关联上一步创建的网关产品。|
        |设备名称|为该网关设备命名。设备名称需保持产品内唯一。如不填写，系统将自动生成。 **说明：** 设备名称支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

 |

    6.  根据所搭建的环境，选择对应的Link IoT Edge产品规格，详细介绍请参见[产品规格](../cn.zh-CN/产品简介/产品规格.md#)。
    7.  （可选）在新增实例页面，单击**新增标签**，可以设置实例标签。通过标签您可以更加有效地归类及识别实例。您也可以不设置标签。
3.  实例参数设置完成后，单击**确定**，至此您已创建边缘实例和网关。
4.  在**实例详情** \> **网关**页面，单击网关名称右侧的**查看**，获取网关设备信息。 

    ![查看网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163487/156618511548695_zh-CN.png)

    系统跳转到网关设备的设备详情页面，在设备详情页面获取网关设备的设备证书（ProductKey、DeviceName、DeviceSecret），用于后续启动Link IoT Edge。

    ![查看网关设备三元组](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163487/156618511548696_zh-CN.png)


## 启动Link IoT Edge {#section_n2l_4ax_8u0 .section}

1.  登录您MacOS系统的设备。
2.  打开如下图所示设备本地终端。 

    ![mac本地终端](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149667/156618511641612_zh-CN.png)

3.  从[下载地址](../cn.zh-CN/产品简介/发布历史/下载地址.md#)轻量版中，下载使用环境为MacOS的Link IoT Edge轻量版软件包，保存到设备本地目录。 例如，下载v1.8.2版本LE Lite软件包到~/Desktop目录，则在本地终端执行如下命令。

    ``` {#codeblock_0tw_qus_njc}
    cd ~/Desktop
    ls -alh link-iot-edge-lite-macos-x86-64-v1.8.2.zip
    ```

4.  解压软件包，可以解压到任意目录。 例如，将已下载完成的v1.8.2版本LE Lite软件包解压到~/Desktop目录，则执行如下命令。

    ``` {#codeblock_lr9_rq9_bb5}
    tar xopfv link-iot-edge-lite-macos-x86-64-v1.8.2.zip
    ```

5.  启动Link IoT Edge。 Link IoT Edge启动脚本在软件包/linkedge/gateway/build/script目录下，因此若要启动上述示例中已解压的v1.8.2版本LE Lite，则执行如下命令。

    ``` {#codeblock_vln_ivm_776}
    cd ~/Desktop/linkedge/gateway/build/script
    ./iot_gateway_start_lite.sh {YourProductKey} {YourDeviceName} {YourDeviceSecret}
    ```

    **说明：** 请将\{YourProductKey\} \{YourDeviceName\} \{YourDeviceSecret\}替换为已获取的网关设备的设备证书信息。

    例如，网关设备证书信息为ProductKey：a1\*\*\*\*\*\*gs、DeviceName：gateway、DeviceSecret：2Px\*\*\*\*\*\*\*\*\*\*\*\*\*\*H1S，则执行的实际命令如下：

    ``` {#codeblock_6j1_0yq_94i}
    
    ./iot_gateway_start_lite.sh a1******gs gateway 2Px**************H1S
    ```

    若系统显示如下信息，表示Link IoT Edge核心服务启动成功。

    ![LE启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149667/156618511641645_zh-CN.png)

    您也可以在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例** ，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618511648694_zh-CN.png)


## 下一步 {#section_91r_abu_43j .section}

1.  **实例详情**页面选择**设置**页签，并在实例信息下，打开远程调试后的按钮。
2.  **实例详情**页面选择**网关**页签，在网关名称右侧的操作栏中单击**远程连接**、**远程文件管理**或者**更多远程服务**，远程控制网关设备或对网关设备上的文件进行管理。详细说明请参见[远程服务访问](../cn.zh-CN/用户指南/远程运维管理/远程服务访问.md#)。

