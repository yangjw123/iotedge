# 基于Windows搭建环境 {#task_1495784 .task}

本文介绍基于Windows系统搭建Link IoT Edge轻量版本（LE Lite）运行环境的方法。

Link IoT Edge轻量版版软件包支持在Windows 7和 Windows 10版本32/64位系统上运行，并在下列平台上进行测试和验证。

|架构|操作系统|
|--|----|
|Windows|Windows 7 32位|
|Windows 7 64位|
|Windows 10 32位|
|Windows 10 64位|

## 前提条件 {#section_dak_ea0_uak .section}

-   当前软件包在Windows机器上的安装，大概需要占用200 MB左右的硬盘资源，请确保硬盘剩余资源足够。
-   Windows机器需要预先配置远程桌面服务，否则无法远程访问。详细配置请参考[微软官方文档](https://support.microsoft.com/zh-cn/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection)。

    ![Windows预置远程桌面服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580341286_zh-CN.png)


## 创建边缘实例和网关 {#section_lfh_y3b_08w .section}

1.  [物联网平台控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例**。
2.  创建一个边缘实例。 
    1.  单击**新增实例**，在弹出窗口中设置**实例名称**。
    2.  在**网关产品**后单击**新建网关产品**，为实例创建网关。 物联网边缘计算中的网关，承载边缘计算能力，每个实例必须分配一个网关设备，并且该网关设备同一时间只能被分配到一个边缘实例。

        ![创建网关产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618580437158_zh-CN.png)

    3.  在新建产品页面中，设置网关产品参数，然后单击**完成**。 物联网边缘计算中的新建网关产品继承物联网平台 **设备管理** \> **产品**中的产品功能，已自动为您简化创建适合物联网边缘计算中使用的网关产品步骤。

        ![创建产品](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618580437159_zh-CN.png)

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

        ![新建网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618580437160_zh-CN.png)

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

    ![查看网关设备](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163487/156618580448695_zh-CN.png)

    系统跳转到网关设备的设备详情页面，在设备详情页面获取网关设备的设备证书（ProductKey、DeviceName、DeviceSecret），用于后续启动Link IoT Edge。

    ![查看网关设备三元组](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163487/156618580448696_zh-CN.png)


## 启动Link IoT Edge {#section_n2l_4ax_8u0 .section}

1.  在左侧导航栏中选择**边缘计算** \> **边缘实例**，单击实例名称右侧的**下载**。 

    ![下载命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/102593/156618580544201_zh-CN.png)

2.  根据环境设置下载参数，然后单击**生成命令**。 

    ![生成命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580551625_zh-CN.png)

    |参数|描述|
    |--|--|
    |CPU架构|您的设备系统对应的CPU架构。此处选择x86。|
    |产品规格|在创建边缘实例时，已选择实例中使用的Link IoT Edge版本。此处不可操作。|
    |边缘版本|选择Link IoT Edge的[发布版本](../cn.zh-CN/产品简介/发布历史/轻量版.md#)。|
    |操作系统|选择您的设备对应的操作系统。此处选择Windows|

3.  下载Windows操作系统安装包备用。 

    ![下载软件包](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580551627_zh-CN.png)

    下载安装包后如下所示。

    ![本地下载包](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580541285_zh-CN.png)

4.  登录您Windows 7版本64位系统的机器。
5.  解压已下载的Link IoT Edge轻量版软件包。
6.  在解压后的目录中找到后缀名为 .exe的可执行程序后双击程序启动Link IoT Edge轻量版。
7.  在阿里云IoT边缘计算远程访问服务界面，输入已在本地保存的网关设备的设备证书信息，并单击左上角启动按钮。 

    ![启动轻量版Windows环境LE](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580641396_zh-CN.png)

    系统显示如下信息，表示已启动成功。

    ![启动成功后](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580641287_zh-CN.png)

    **说明：** Windows版本默认访问本地3389端口的远程桌面服务，暂不支持端口配置。

    您也可以在[物联网控制台](http://iot.console.aliyun.com/)，选择 **边缘计算** \> **边缘实例** ，在已创建好的边缘实例右侧单击**查看**进入**实例详情**页面，选择**网关**，查看网关状态。

    ![网关在线](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/104167/156618580648694_zh-CN.png)


## 远程访问 {#section_vxn_o97_0np .section}

1.  打开远程访问助手，输入远程连接信息。详细使用说明请参考[远程访问助手](cn.zh-CN/用户指南/远程运维管理/远程访问助手.md#)。 

    ![打开远程助手](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580741398_zh-CN.png)

    |参数|描述|
    |--|--|
    |ProductKey|填写已在本地保存的网关设备的设备证书信息中ProductKey的值。|
    |DeviceName|填写已在本地保存的网关设备名称。|
    |远程服务类型|选择**远程桌面（RDP）**。|
    |远程服务端口|必须填写为Windows版本默认访问本地3389端口。 **说明：** 切勿修改远程服务端口，否则将导致Link IoT Edge不可用。

 |

2.  配置远程桌面工具。 

    ![配置远程桌面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580741580_zh-CN.png)

    您需要配置如下参数，其余用默认值。

    |参数|说明|
    |--|--|
    |Connection name|连接名称，您可以自定义。|
    |PC name|远程主机的名称，格式必须为`127.0.0.1:xxxx`。 其中，`xxxx`是远程访问助手上显示的本地端口号。

 |

3.  参数配置完成后单击**Start**，运行远程桌面。设备的远程桌面如下图所示，您可以使用鼠标和键盘进行操作。 

    ![启动成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147481/156618580741581_zh-CN.png)


