# ClearEdgeInstanceDriverConfigs {#reference_878629 .reference}

调用该接口清空边缘实例驱动配置。

## 限制说明 {#section_ss0_imp_xxi .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_4ag_0mk_fmr .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：ClearEdgeInstanceDriverConfigs。|
|InstanceId|String|是|边缘实例ID。|
|DriverId|String|是|驱动ID。|
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_4zi_sii_s4i .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|

## 示例 {#section_qvi_5sj_ucy .section}

请求示例

``` {#codeblock_bw3_wuv_gqd}
https://iot.cn-shanghai.aliyuncs.com/?Action=ClearEdgeInstanceDriverConfigs
&DriverId=021d154d2a2f4dd7a489773d9e04****
&InstanceId=F3APY0tPLhmgGtx0****
&公共参数
```

返回示例

-   JSON格式

    ``` {#codeblock_k35_8dq_jnm}
    {
     "RequestId": "DF6B728B-ADD7-4C41-88C3-D21B4CA82CF1",
     "Code": "Success",
     "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_jgf_o7g_gjd}
    <?xml version="1.0" encoding="UTF-8"?>
    <ClearEdgeInstanceDriverConfigsResponse>
        <RequestId>DF6B728B-ADD7-4C41-88C3-D21B4CA82CF1</RequestId>
        <Code>Success</Code>
        <Success>true</Success>
    </ClearEdgeInstanceDriverConfigsResponse>
    ```


