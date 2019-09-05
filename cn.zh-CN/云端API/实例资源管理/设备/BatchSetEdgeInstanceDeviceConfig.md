# BatchSetEdgeInstanceDeviceConfig {#reference_878641 .reference}

调用该接口批量配置边缘实例设备。

## 限制说明 {#section_r3g_hiw_kni .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_bkg_4jl_45r .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：BatchSetEdgeInstanceDeviceConfig。|
|InstanceId|String|是|边缘实例ID。|
|DeviceConfigs|List|是|设备配置信息。详情请参见下表DeviceConfigs。 单次调用最多可配置20个设备信息。

 |
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|IotId|String|是|设备ID。 可调用[QueryEdgeInstanceDevice](cn.zh-CN/云端开发指南/云端API参考/边缘实例管理/QueryEdgeInstanceDevice.md#)查询实例中的设备ID。

 |
|Content|String|是|配置内容，可以选择传入： -   配置内容文本。
-   存储配置文件的阿里云对象存储（OSS）地址。

 |

## 返回参数 {#section_vpy_34t_6oy .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|

## 示例 {#section_d88_nk1_zst .section}

请求示例

``` {#codeblock_krk_fno_q9m}
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchSetEdgeInstanceDeviceConfig
&InstanceId=F3APY0tPLhmgGtx0****
&DeviceConfigs.1.IotId=sjI0Sd124XFYyjBY****000101
&DeviceConfigs.2.IotId=BXPV9Ks3bxwM9fD****0000101
&DeviceConfigs.1.Content={"test": "device_config_demo"}
&DeviceConfigs.2.Content={"test": "device_config_demo"}
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_sgw_5zj_irg}
    {
     "RequestId": "748659E2-EDC9-4E3E-BF9D-06F16995CF66",
     "Code": "Success",
     "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_oqj_a79_1pb}
    <?xml version="1.0" encoding="UTF-8"?>
    <BatchSetEdgeInstanceDeviceConfigResponse>
        <RequestId>748659E2-EDC9-4E3E-BF9D-06F16995CF66</RequestId>
        <Code>Success</Code>
        <Success>true</Success>
    </BatchSetEdgeInstanceDeviceConfigResponse>
    ```


