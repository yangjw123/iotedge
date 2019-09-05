# QueryEdgeInstanceGateway {#concept_878619 .concept}

调用该接口查询边缘实例中的网关。

## 限制说明 {#section_mui_mzr_5cd .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_ru0_9yl_hyp .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：QueryEdgeInstanceGateway。|
|InstanceId|String|是|边缘实例ID。|
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_cv7_sfw_1cv .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|
|GatewayList|List|调用成功时，返回的网关数据。详情请参见下表Gateway。|

|名称|类型|描述|
|:-|:-|:-|
|ProductKey|String|网关所属的产品Key，产品的唯一标识符。|
|DeviceName|String|网关设备名称。|
|IotId|String|网关设备的ID，物联网平台为设备生成的唯一标识符。|
|EdgeVersion|String|边缘服务版本号。|

## 示例 {#section_pou_gl2_xf4 .section}

请求示例

``` {#codeblock_5hx_rip_uyt}
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryEdgeInstanceGateway
&InstanceId=F3APY0tPLhmgGtx0****
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_rip_wpt_zbb}
    {
      "GatewayList": [
        {
          "IotId": "LuD9x5hiRUdVemWU****000101",
          "ProductKey": "a1mAdeG****",
          "DeviceName": "e46ea1a4347c42a0a83b8c956ab1ab",
          "EdgeVersion": "v1.0.0"
        }
      ],
      "RequestId": "547A62E5-0D6D-4DB5-9CCC-58C706891976",
      "Code": "Success",
      "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_egn_obr_jsk}
    <?xml version="1.0" encoding="UTF-8"?>
    <QueryEdgeInstanceGatewayResponse>
      <GatewayList>
        <Gateway>
          <IotId>LuD9x5hiRUdVemWU****000101</IotId>
          <ProductKey>a1mAdeG****</ProductKey>
          <DeviceName>e46ea1a4347c42a0a83b8c956ab1ab</DeviceName>
          <EdgeVersion>v1.0.0</EdgeVersion>
        </Gateway>
      </GatewayList>
      <RequestId>547A62E5-0D6D-4DB5-9CCC-58C706891976</RequestId>
      <Code>Success</Code>
      <Success>true</Success>
    </QueryEdgeInstanceGatewayResponse>
    ```


