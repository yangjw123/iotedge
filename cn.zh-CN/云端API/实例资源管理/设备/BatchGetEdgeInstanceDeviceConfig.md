# BatchGetEdgeInstanceDeviceConfig {#reference_878643 .reference}

调用该接口批量获取边缘实例设备配置。

## 限制说明 {#section_brt_e20_y6e .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_te3_d1i_mme .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：BatchGetEdgeInstanceDeviceConfig。|
|InstanceId|String|是|边缘实例ID。|
|IotIds|List<String\>|是|要查询的设备ID列表。最多可传入20个设备ID。 可调用[QueryEdgeInstanceDevice](cn.zh-CN/云端开发指南/云端API参考/边缘实例管理/QueryEdgeInstanceDevice.md#)查询边缘实例中的设备信息列表，获取设备IotId。

 |
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_6z7_jou_ymh .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|
|DeviceConfigList|List|调用成功时，返回的设备配置数据。详情请参见下表DeviceConfig。|

|名称|类型|描述|
|:-|:-|:-|
|IotId|String|设备ID。|
|Config|Struct|设备配置信息，详情请参见下表Config。|

|名称|类型|描述|
|:-|:-|:-|
|Format|String|配置文件格式：KV、JSON、或FILE。|
|Content|String|配置内容文本或存储配置内容文件的OSS地址。|

## 示例 {#section_5iu_dlq_ceb .section}

请求示例

``` {#codeblock_for_3vv_lts}
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetEdgeInstanceDeviceConfig
&IotIds.2=BXPV9Ks3bxwM9fDl****000101
&IotIds.1=sjI0Sd124XFYyjBY****000101
&InstanceId=F3APY0tPLhmgGtx0****
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_5w6_a7h_tbh}
    {
      "DeviceConfigList": [
        {
          "IotId": "sjI0Sd124XFYyjBY****000101",
          "Config": {
            "Format": "JSON",
            "Content": "{\"test\": \"device_config_demo\"}"
          }
        },
        {
          "IotId": "BXPV9Ks3bxwM9fD****0000101",
          "Config": {
            "Format": "JSON",
            "Content": "{\"test\": \"device_config_demo\"}"
          }
        }
      ],
      "RequestId": "D4A102C2-36A5-4964-9694-0F8EFF95CCA8",
      "Code": "Success",
      "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_eqq_lpb_mz5}
    <?xml version="1.0" encoding="UTF-8"?>
    <BatchGetEdgeInstanceDeviceConfigResponse>
      <DeviceConfigList>
        <DeviceConfig>
          <IotId>sjI0Sd124XFYyjBY****000101</IotId>
          <Config>
            <Format>JSON</Format>
            <Content>{"test": "device_config_demo"}</Content>
          </Config>
        </DeviceConfig>
        <DeviceConfig>
          <IotId>BXPV9Ks3bxwM9fD****0000101</IotId>
          <Config>
            <Format>JSON</Format>
            <Content>{"test": "device_config_demo"}</Content>
          </Config>
        </DeviceConfig>
      </DeviceConfigList>
      <RequestId>D4A102C2-36A5-4964-9694-0F8EFF95CCA8</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
    </BatchGetEdgeInstanceDeviceConfigResponse>
    ```


