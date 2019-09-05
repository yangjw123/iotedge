# SetEdgeInstanceDriverConfigs {#reference_878628 .reference}

调用该接口配置边缘实例驱动。

## 限制说明 {#section_249_dbt_fu0 .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_c72_izu_ih5 .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：SetEdgeInstanceDriverConfigs。|
|InstanceId|String|是|边缘实例ID。|
|DriverId|String|是|驱动ID。|
|Configs|List|是|配置信息。详情请参见下表Configs。|
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Format|String|是|配置文件格式，可选值： KV、JSON、FILE。|
|Content|String|是|配置内容，可以选择传入： -   配置内容文本。
-   存储配置文件的阿里云对象存储（OSS）地址。

 |
|Key|String|否|配置的关键字。在有多个配置的情况下，用于区分配置。|

## 返回参数 {#section_nnv_dy2_sni .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|

## 示例 {#section_6r6_0nn_umb .section}

请求示例

``` {#codeblock_lrs_8yt_2bl}
https://iot.cn-shanghai.aliyuncs.com/?Action=SetEdgeInstanceDriverConfigs
&Configs.1.Content={"test":123}
&DriverId=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&Configs.1.Format=JSON
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_mdk_5dg_cox}
    {
     "RequestId": "252C7754-F6A2-454B-9DE2-382A97FC0C3F",
     "Code": "Success",
     "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_450_12t_18u}
    <?xml version="1.0" encoding="UTF-8"?>
    <SetEdgeInstanceDriverConfigsResponse>
        <RequestId>252C7754-F6A2-454B-9DE2-382A97FC0C3F</RequestId>
        <Code>Success</Code>
        <Success>true</Success>
    </SetEdgeInstanceDriverConfigsResponse>
    ```


