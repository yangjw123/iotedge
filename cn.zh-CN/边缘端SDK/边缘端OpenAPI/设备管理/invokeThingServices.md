# invokeThingServices {#reference_mtx_bxl_jhb .reference}

POST /thing/device/service/invoke

## 功能描述 {#section_xwn_bvh_x2w .section}

设备的服务调用。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|productKey|String|是|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|inputParams|Json|是|服务入参。必须与在物联网平台控制台，为设备所属产品自定义产品功能时设置的，服务输入参数名称保持一致。|
|method|String|是|服务方法。 必须与在物联网平台控制台，为设备所属产品定义产品功能时设置的 ，服务标识符保持一致。|
|deviceName|String|是|设备的名称。可从物联网平台控制台获取。|

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "data": null,
        "message": "success"
    }
    ```

-   异常返回示例

    ```
    {
      "code": 400,
      "data": null,
      "message": "device not found"
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": { \"productKey\": \"a1VCsnA****\", \"deviceName\": \"Led****\", \"method\": \"power_on\", \"inputParams\": {\"a\": \"1234abc\"}}}" -k -X POST https://127.0.0.1:9999/thing/device/service/invoke
# 输出
{
    "code":200,
    "message":"success",
    "data":{
        "code":0,
        "data":{
            "rtn":"asdfasdf",
            "uid":"111",
            "code":1
        },
        "message":"ok"
    }
}
```

