# getThingsEventsInfo {#reference_ovt_dxl_jhb .reference}

POST /thing/device/events/get

## 功能描述 {#section_xwn_bvh_x2w .section}

订阅设备事件。该接口会保持长连接且不可被重复使用，若有设备事件上报，则在本接口中返回给接口调用者。

**说明：** 该接口支持订阅多个设备的多个事件。

该接口保持长连接时，返回消息的格式为`$Length\r\n\$content$Length\r\n$content`，即由消息内容长度的16进制、1个`\r\n`、实际消息体组成。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|eventInfo|Json|是|请求参数列表。若取值为`[]`，则返回所有设备的所有事件。必须符合Json数组格式，每组必须包含`productKey`、`deviceName`和`eventIdentifier`三个key。具体格式请见请求示例。|

## 请求示例 {#section_t3t_ygz_khb .section}

```
"eventinfo": [{
    "productKey": "aaa", //设备的productKey, 用户可以物联网平台设备管理->设备信息页找到设备的 ProductKey 。
    "deviceName": "bbb1", //设备名称。用户可以在物联网平台设备管理－>设备信息页找到设备的DeviceName 。
    "eventIdentifier": [//物的事件标识符;非必填，为空返回所有事件; 有值则与用户在物联网平台创建产品定义产品功能时录入的自定义事件名称保持一致。
      "aaaa", "bbbb", "ccc"
    ]
  },
  {
    "productKey": "aaa",
    "deviceName": "bbb2",
    "eventIdentifier": [//物的事件标识符;非必填，为空返回所有事件;
      "aaaa", "bbbb", "ccc"
    ]
  },
  {
    "productKey": "aaa",
    "deviceName": "bbb3",
    "eventIdentifier": [//物的事件标识符;非必填，为空返回所有事件;
      "aaaa", "bbbb", "ccc"
    ]
  }
]
```

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "message": "success",
        "data": {
            "items": {
                "productKey": string,
                "deviceName": string,
                "eventCode": "Error",
                "iotId": "",                        //注意，iotId 在边缘端为空。
                "eventName": "aaaaa",           
                "eventType": "info",                
                "eventBody": {
                    "ErrorCode": 0
                },
                "batchId": "",                      //注意，batchId 在边缘端为空。
                "timestamp": 1516342985261
            },
            "timestamp": 1516343075699
        }
    }
    //注意，考虑到这里是长连接，由server主动推给client，开发者需要关注Http header里面的Transfer-Encoding:chunked字段。
    ```

-   异常返回参数示例

    ```
    {
      "code": 401,
      "data": null,
      "message": "device not found"
    }
    ```

-   心跳返回示例

    ``` {#codeblock_4z5_ivv_qgr}
    {
        "code":204,
        "message":"heartbeats",
        "data":null
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": {\"eventInfo\": [{ \"productKey\": \"a1JJ3QE****\", \"deviceName\": \"1njlnxNbdHs4EmOh****\", \"eventIdentifier\": [\"abc\", \"edf\"]}, { \"productKey\": \"a1JJ3QE****\", \"deviceName\": \"8sQa2kvLKpWitIFF****\", \"eventIdentifier\": [\"abc\", \"edf\"]}]}}" -k -X POST https://127.0.0.1:9999/thing/device/events/get
# 输出
34
{
    "code":204,
    "message":"heartbeats",
    "data":null
}
34
{
    "code":204,
    "message":"heartbeats",
    "data":null
}
151
{
    "code":200,
    "data":{
        "timestamp":"",
        "items":{
            "productKey":string,
            "deviceName":string,
            "iotId":"",
            "eventBody":{
                "params":{
                    "value":{
                        "timestamp":"88888",
                        "markingTime":66666,
                        "designName":"this is design name"
                    },
                    "time":1535206490271
                }
            },
            "eventType":"machinestatuschange",
            "batchId":"",
            "eventName":"machinestatuschange",
            "eventCode":"",
            "timestamp":""
        }
    },
    "message":"success"
}
151
{
    "code":200,
    "data":{
        "timestamp":"",
        "items":{
            "productKey":string,
            "deviceName":string,
            "iotId":"",
            "eventBody":{
                "params":{
                    "value":{
                        "timestamp":"88888",
                        "markingTime":66666,
                        "designName":"this is design name"
                    },
                    "time":1535206491073
                }
            },
            "eventType":"machinestatuschange",
            "batchId":"",
            "eventName":"machinestatuschange",
            "eventCode":"",
            "timestamp":""
        }
    },
    "message":"success"
}
151
{
    "code":200,
    "data":{
        "timestamp":"",
        "items":{
            "productKey":string,
            "deviceName":string,
            "iotId":"",
            "eventBody":{
                "params":{
                    "value":{
                        "timestamp":"88888",
                        "markingTime":66666,
                        "designName":"this is design name"
                    },
                    "time":1535206492272
                }
            },
            "eventType":"machinestatuschange",
            "batchId":"",
            "eventName":"machinestatuschange",
            "eventCode":"",
            "timestamp":""
        }
    },
    "message":"success"
}
151
{
    "code":200,
    "data":{
        "timestamp":"",
        "items":{
            "productKey":string,
            "deviceName":string,
            "iotId":"",
            "eventBody":{
                "params":{
                    "value":{
                        "timestamp":"88888",
                        "markingTime":66666,
                        "designName":"this is design name"
                    },
                    "time":1535206493074
                }
            },
            "eventType":"machinestatuschange",
            "batchId":"",
            "eventName":"machinestatuschange",
            "eventCode":"",
            "timestamp":""
        }
    },
    "message":"success"
}
151
{
    "code":200,
    "data":{
        "timestamp":"",
        "items":{
            "productKey":string,
            "deviceName":string,
            "iotId":"",
            "eventBody":{
                "params":{
                    "value":{
                        "timestamp":"88888",
                        "markingTime":66666,
                        "designName":"this is design name"
                    },
                    "time":1535206494272
                }
            },
            "eventType":"machinestatuschange",
            "batchId":"",
            "eventName":"machinestatuschange",
            "eventCode":"",
            "timestamp":""
        }
    },
    "message":"success"
}
```

