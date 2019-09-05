# CreateEdgeInstanceDeployment {#reference_878645 .reference}

调用该接口创建边缘实例部署单。

## 限制说明 {#section_032_90d_m69 .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_upu_4p0_jsn .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：CreateEdgeInstanceDeployment。|
|InstanceId|String|是|边缘实例ID。|
|Type|String|是|部署单类型。 -   deploy：部署。
-   reset：重置。

 |
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_bjg_oq0_v84 .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|
|DeploymentId|String|调用成功时，返回的部署任务单ID。|

## 示例 {#section_oqa_o59_19y .section}

请求示例

``` {#codeblock_r4t_ug1_3qt}
https://iot.cn-shanghai.aliyuncs.com/?Action=CreateEdgeInstanceDeployment
&InstanceId=PgEfYupSn6Pvhfkx****
&Type=deploy
&公共请求参数
```

返回示例

-   JSON格式

    ``` {#codeblock_ska_d8r_53z}
    {
      "RequestId": "C8293A57-6BBC-42FB-B093-BF304D5BF09C",
      "DeploymentId": "38d544b1222d45b4b425240167bf****",
      "Code": "Success",
      "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_sup_byv_u06}
    <?xml version="1.0" encoding="UTF-8"?>
    <CreateEdgeInstanceDeploymentResponse>
        <RequestId>C8293A57-6BBC-42FB-B093-BF304D5BF09C</RequestId>
        <DeploymentId>38d544b1222d45b4b425240167bf****</Data>
        <Code>Success</Code>
        <Success>true</Success>
    </CreateEdgeInstanceDeploymentResponse>
    ```


