# getThingProperties {#reference_ppl_xwl_jhb .reference}

POST /thing/device/property/query

## 功能描述 {#section_xwn_bvh_x2w .section}

获取设备的实时属性值。调用该接口会直接把请求下发到设备上。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|productKey|String|是|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|deviceName|String|是|设备的名称。可从物联网平台控制台获取。|
|propertyIdentifier|JsonArray|是|设备的属性标识符。格式如下： ```
[
    "cpu_core_number",
    "cpu_usage"
]
```

 |

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "message": "success",
        "data": [
            {
                "iotId;": "",                       //注意，iotId 在边缘端为空。
                "batchId": "",                      
                "attribute;": "xxx",                
                "group;": "",                       //注意，group 在边缘端为空。
                "value": "xxxx",
                "gmtModified": 1237891329
            }
        ]
    }
    ```

-   异常返回参数示例

    ```
    {
      "code": 401,
      "data": null,
      "message": "device not found"
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": { \"productKey\": \"a1acbea****\", \"deviceName\": \"RijJCeD63B0DXKQs****\", \"propertyIdentifier\": [\"cpu_core_number\",\"cpu_usage\"]}}" -k -X POST https://127.0.0.1:9999/thing/device/property/query
# 输出
{
    "code":200,
    "message":"success",
    "data":[
        {
            "iotId":"",
            "value":"8",
            "gmtModified":"1552035452",
            "attribute":"cpu_core_number",
            "groud":"",
            "batchId":""
        },
        {
            "iotId":"",
            "value":"16.730524",
            "gmtModified":"1552035452",
            "attribute":"cpu_usage",
            "groud":"",
            "batchId":""
        }
    ]
}
```

