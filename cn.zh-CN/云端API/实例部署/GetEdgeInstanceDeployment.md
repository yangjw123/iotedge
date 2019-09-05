# GetEdgeInstanceDeployment {#reference_878651 .reference}

调用该接口获取边缘实例部署单详情。

## 限制说明 {#section_9db_g77_9xl .section}

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

    **说明：** 子账号共享主账号配额。

-   单客户端出口IP的最大QPS限制为100，即来自单个客户端出口IP，调用阿里云接口的每秒请求总数不能超过100。

## 请求参数 {#section_hso_9dq_d4d .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：GetEdgeInstanceDeployment。|
|InstanceId|String|是|边缘实例ID。|
|DeploymentId|String|是|部署单ID。|
|公共请求参数|-|是|公共请求参数，请参见[公共参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#) 。|

## 返回参数 {#section_ins_mhe_aqv .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。true表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|Code|String|接口返回码。|
|Data|Struct|调用成功时，返回的数据。详情请参见下表Data。|

|名称|类型|描述|
|:-|:-|:-|
|GmtCreate|String|部署单创建时间。|
|GmtModified|String|部署单最后一次更新时间。|
|GmtCompleted|String|完成时间。|
|DeploymentId|String|部署单ID。|
|Description|String|实例描述。|
|Status|Integer|部署单当前状态。 -   0：未开始（init）。
-   1：正在进行中（processing）。
-   2：成功（success）。
-   3：失败（failure）。

 |
|Type|String|部署单类型。 -   deploy：部署。
-   reset：重置。

 |
|TaskList|List|部署任务列表，详情请参见下表Task。|

|名称|类型|描述|
|:-|:-|:-|
|GmtCreate|String|部署任务创建时间。|
|GmtModified|String|部署任务最后一次更新时间。|
|GmtCompleted|String|完成时间。|
|GatewayId|String|网关设备ID。|
|TaskId|String|部署任务ID。|
|Stage|Integer|部署任务当前阶段。 -   0：未开始（init）。
-   8：正在装配（assembly）。
-   16：正在打包（package）。
-   24：正在分发（dispatcher）。
-   32：已完成（finish）。

 |
|Status|Integer|部署任务当前状态。 -   0：初始状态（init）。
-   1：正在进行中（processing）。
-   2：成功（success）。
-   3：失败（failure）。

 |
|ResourceSnapshotList|List|部署快照列表，详情请参见下表ResourceSnapshot。|

|名称|类型|描述|
|:-|:-|:-|
|GmtCreate|String|部署单快照创建时间。|
|GmtModified|String|部署单快照最后一次更新时间。|
|GmtCompleted|String|完成时间。|
|SnapshotId|String|部署快照ID。|
|ResourceType|String|资源类型。|
|ResourceId|String|资源ID。|
|ResourceName|String|资源名称。|
|OperateType|Integer|操作类型。 -   0：部署（deploy）。
-   1：删除（delete）。

 |
|Stage|Integer|部署单快照当前阶段。 -   0：初始状态（init）。
-   8：正在编译（assembly）。
-   16：正在打包（package）。
-   24：正在分发（dispatcher）。
-   32：已完成（finish）。

 |
|Status|Integer|当前状态。 -   0：未开始（init）。
-   1：正在进行（processing）。
-   2：成功（success）。
-   3：失败（failure）。

 |
|Log|String|资源部署日志。|

## 示例 {#section_6np_sql_6k0 .section}

请求示例

``` {#codeblock_grz_zhc_mk4}
https://iot.cn-shanghai.aliyuncs.com/?Action=GetEdgeInstanceDeployment
&InstanceId=PgEfYupSn6Pvhfkx****
&DeployId=9261e308a9504fde9b4cf8462b0b****
&公共参数
```

返回示例

-   JSON格式

    ``` {#codeblock_e0x_o6r_y01}
    {
      "RequestId": "6B72291A-9492-445E-81D9-335D2D3E44C0",
      "Data": {
        "Status": 2,
        "DeploymentId": "9261e308a9504fde9b4cf8462b0b****",
        "GmtCompleted": "2019-06-26 18:12:35",
        "Type": "deploy",
        "GmtCreate": "2019-06-26 18:12:29",
        "Description": "deploy_1561543948874",
        "TaskList": [
          {
            "Status": 2,
            "GmtCompleted": "2019-06-26 18:12:35",
            "GmtCreate": "2019-06-26 18:12:29",
            "TaskId": "49ea651529014bf8b5645d5f9062****",
            "ResourceSnapshotList": [
              {
                "Status": 2,
                "SnapshotId": "ab576e84a43043d7840cbcebf4a5****",
                "GmtCompleted": "2019-06-26 18:12:34",
                "GmtCreate": "2019-06-26 18:12:29",
                "Log": "[{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":0,\"level\":\"INFO\",\"message\":\"init success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543949858},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":8,\"level\":\"INFO\",\"message\":\"assembly success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543951419},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":16,\"level\":\"INFO\",\"message\":\"package success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543952591},{\"resourceId\":\"device_config\",\"code\":\"0\",\"stage\":32,\"level\":\"INFO\",\"message\":\"download success\",\"resourceType\":\"DEVICE_CONFIG\",\"timestamp\":1561543954149}]",
                "ResourceId": "device_config",
                "ResourceName": "device_config",
                "GmtModified": "2019-06-26 18:12:34",
                "Stage": 32,
                "ResourceType": "device_config",
                "OperateType": 0
              }
            ],
            "GmtModified": "2019-06-26 18:12:35",
            "Stage": 32,
            "GatewayId": "jQWf3MVgQjMzcwsY****000101"
          }
        ],
        "GmtModified": "2019-06-26 18:12:35"
      },
      "Code": "Success",
      "Success": true
    }
    ```

-   XML格式

    ``` {#codeblock_7lb_74x_qbq}
    <?xml version="1.0" encoding="UTF-8"?>
    <GetEdgeInstanceDeploymentResponse>
      <RequestId>6B72291A-9492-445E-81D9-335D2D3E44C0</RequestId>
      <Data>
        <Status>2</Status>
        <DeploymentId>9261e308a9504fde9b4cf8462b0b****</DeploymentId>
        <GmtCompleted>2019-06-26 18:12:35</GmtCompleted>
        <Type>deploy</Type>
        <GmtCreate>2019-06-26 18:12:29</GmtCreate>
        <Description>deploy_1561543948874</Description>
        <TaskList>
          <Task>
            <Status>2</Status>
            <GmtCompleted>2019-06-26 18:12:35</GmtCompleted>
            <GmtCreate>2019-06-26 18:12:29</GmtCreate>
            <TaskId>49ea651529014bf8b5645d5f9062****</TaskId>
            <ResourceSnapshotList>
              <ResourceSnapshot>
                <Status>2</Status>
                <SnapshotId>ab576e84a43043d7840cbcebf4a5****</SnapshotId>
                <GmtCompleted>2019-06-26 18:12:34</GmtCompleted>
                <GmtCreate>2019-06-26 18:12:29</GmtCreate>
                <Log>[{"resourceId":"device_config","code":"0","stage":0,"level":"INFO","message":"init success","resourceType":"DEVICE_CONFIG","timestamp":1561543949858},{"resourceId":"device_config","code":"0","stage":8,"level":"INFO","message":"assembly success","resourceType":"DEVICE_CONFIG","timestamp":1561543951419},{"resourceId":"device_config","code":"0","stage":16,"level":"INFO","message":"package success","resourceType":"DEVICE_CONFIG","timestamp":1561543952591},{"resourceId":"device_config","code":"0","stage":32,"level":"INFO","message":"download success","resourceType":"DEVICE_CONFIG","timestamp":1561543954149}]</Log>
                <ResourceId>device_config</ResourceId>
                <ResourceName>device_config</ResourceName>
                <GmtModified>2019-06-26 18:12:34</GmtModified>
                <Stage>32</Stage>
                <ResourceType>device_config</ResourceType>
                <OperateType>0</OperateType>
              </ResourceSnapshot>
            </ResourceSnapshotList>
            <GmtModified>2019-06-26 18:12:35</GmtModified>
            <Stage>32</Stage>
            <GatewayId>jQWf3MVgQjMzcwsY****000101</GatewayId>
          </Task>
        </TaskList>
        <GmtModified>2019-06-26 18:12:35</GmtModified>
      </Data>
      <Code>Success</Code>
      <Success>true</Success>
    </GetEdgeInstanceDeploymentResponse>
    ```


