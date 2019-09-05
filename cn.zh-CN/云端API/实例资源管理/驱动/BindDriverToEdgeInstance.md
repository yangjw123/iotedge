# BindDriverToEdgeInstance {#reference_878622 .reference}

调用该接口将驱动分配到边缘实例中。

## 限制说明 {#section_uju_3vq_o04 .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_fqn_yqx_ock .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：BindDriverToEdgeInstance。|
|InstanceId|String|是|边缘实例ID。|
|DriverId|String|是|驱动ID。|
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_1cp_02w_r4s .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。200表示成功，其它表示错误码。|

## 示例 {#section_lx1_qke_33z .section}

请求示例

``` {#codeblock_umt_kmr_avf}
https://iot.cn-shanghai.aliyuncs.com/?Action=BindDriverToEdgeInstance
&DriverId=9c1ae7bd59f1469abbdccc959228****
&InstanceId=F3APY0tPLhmgGtx0****
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_tex_vdz_q8l}
    {
     "RequestId": "FEA6A369-2E16-4DB3-A0A6-6D14FD244170",
     "Code": "Success",
     "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_bpy_fhj_thy}
    <?xml version="1.0" encoding="UTF-8"?>
    <BindDriverToEdgeInstanceResponse>
        <RequestId>FEA6A369-2E16-4DB3-A0A6-6D14FD244170</RequestId>
        <Code>Success</Code>
        <Success>true</Success>
    </BindDriverToEdgeInstanceResponse>
    ```


