# getAuthedDeviceList {#reference_rxx_5wl_jhb .reference}

POST /thing/device/list-authed

## 功能描述 {#section_xwn_bvh_x2w .section}

获取已认证设备的列表。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|productKey|String|否|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|driverName|String|否|分配到设备的驱动名称。取值为： -   官方驱动名称Modbus或OPCUA。
-   在物联网平台控制台，**边缘计算** \> **驱动管理**中自定义的驱动名称。

 |
|DeviceTags|Json|否|设备标签列表。可从物联网平台控制台获取。|
|LocalState|String|否|设备本地在线状态。取值如下： -   Online：在线
-   Offline：离线

 |
|CloudState|String|否|设备云端在线状态。取值如下： -   Inactive：未激活
-   ActivationFailed：激活失败
-   Online：在线
-   Offline：离线

 |
|PageSize|Intger|是|指定返回结果中每页显示的记录数量。如果取值为0， 则返回所有设备列表。|
|CurrentPage|Intger|是|指定显示返回结果中的第几页的内容。默认值为 1。|
|SortMethod|String|否|返回结果中设备的排序方式。以设备创建的时间顺序排序，取值如下： -   TimeDesc：倒序
-   TimeAsc：正序

 默认为时间倒序排序。

 |

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "data": {
        "TotalNum": int,
        "PageSize": int,
        "CurrentPage": int, //从1开始计算
        "List": [
              //LocalState: [Inactive, ActivationFailed, Online, Offline], Inactive，未激活；ActivationFailed，激活失败；Online，本地在线；Offline，本地离线
              //CloudState: [Inactive, ActivationFailed, Online, Offline], Inactive，未激活；ActivationFailed，激活失败；Online，云端在线；Offline，云端离线
              //DeviceLocalId: 设备注册时传入的设备名称
              //DeviceName: 设备注册成功后，分配的云端显示的设备名称(三元组里的device name)
              {"ProductKey": string, "DeviceName": string, "DriverName": string, "DeviceLocalId": string, "DeviceTags": [string, string, string], "LocalState": string, "CloudState": string, "LastLocalOnlineTime": string, "LastCloudOnlineTime": string, "DeviceLocalId": "abcabcedfg2"},
              {"ProductKey": string, "DeviceName": string, "DriverName": string, "DeviceLocalId": string, "DeviceTags": [string, string, string], "LocalState": string, "CloudState": string, "LastLocalOnlineTime": string, "LastCloudOnlineTime": string, "DeviceLocalId": "abcabcedfg2"},
              {"ProductKey": string, "DeviceName": string, "DriverName": string, "DeviceLocalId": string, "DeviceTags": [string, string, string], "LocalState": string, "CloudState": string, "LastLocalOnlineTime": string, "LastCloudOnlineTime": string, "DeviceLocalId": "abcabcedfg2"}
            ]
        },
        "message": "success"
    }
    ```

-   异常返回示例

    ```
    {
      "code": 403,
      "data": null,
      "message": "device not found"
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": {\"PageSize\": 15, \"CurrentPage\": 1}}" -k -X POST https://127.0.0.1:9999/thing/device/list-authed
# 输出
{
    "code":200,
    "message":"success",
    "data":{
        "List":[
            {
                "LocalState":"Offline",
                "DriverName":"websocket",
                "LastCloudOnlineTime":"1536538951000",
                "DeviceName":"F3eKBL2fLEQxSSh2****",
                "CloudState":"Offline",
                "DeviceTags":[
                ],
                "LastLinkTime":"1536538951000",
                "ProductKey":"a1JJ3QE****",
                "LastLocalOnlineTime":"1536538951000",
                "DeviceLocalId":"abcabcedfg2"
            },
            {
                "LocalState":"Offline",
                "DriverName":"websocket",
                "LastCloudOnlineTime":"1536538950000",
                "DeviceName":"bdzP2VNc6mSaaY3U****",
                "CloudState":"Offline",
                "DeviceTags":[
                ],
                "LastLinkTime":"1536538950000",
                "ProductKey":"a1JJ3QE****",
                "LastLocalOnlineTime":"1536538950000",
                "DeviceLocalId":"abcabcedfg1"
            },
            {
                "LocalState":"Offline",
                "DriverName":"websocket",
                "LastCloudOnlineTime":"1536538490000",
                "DeviceName":"B62SxMDuQ3oWoqAJ****",
                "CloudState":"Offline",
                "DeviceTags":[
                ],
                "LastLinkTime":"1536538490000",
                "ProductKey":"a1JJ3QE****",
                "LastLocalOnlineTime":"1536538490000",
                "DeviceLocalId":"abcabcedfg0"
            },
            {
                "LocalState":"Online",
                "DriverName":"gateway_monitor",
                "LastCloudOnlineTime":"1536344986000",
                "DeviceName":"openapi_gw****",
                "CloudState":"Online",
                "DeviceTags":[
                ],
                "LastLinkTime":"1536344986000",
                "ProductKey":"b1xONOb****",
                "LastLocalOnlineTime":"1536344986000",
                "DeviceLocalId":"openapi_gw****"
            }
        ],
        "CurrentPage":1,
        "TotalNum":4,
        "PageSize":15
    }
}
```

