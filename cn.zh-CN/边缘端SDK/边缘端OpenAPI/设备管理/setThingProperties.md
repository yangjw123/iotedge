# setThingProperties {#reference_dx2_wwl_jhb .reference}

POST /thing/device/properties/set

## 功能描述 {#section_xwn_bvh_x2w .section}

设置设备的属性。调用该接口后属性值将直接下发到设备上。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|productKey|String|是|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|deviceName|String|是|设备的名称。可从物联网平台控制台获取。|
|properties|Json|是|设备的属性列表。格式如下： ```
{
    "cpu_core_number":1,
    "aaa":2
}
```

 |

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "data": null
    }
    ```

-   异常返回示例

    ```
    {
      "code": 403,
      "data": null
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": { \"productKey\": \"a1VCsnA****\", \"deviceName\": \"cloud_sync_****\", \"properties\": {\"cpu_core_number\": 1, \"aaa\": 2} }}" -k -X POST https://127.0.0.1:9999/thing/device/properties/set
# 输出
{
    "code":200,
    "message":"success",
    "data":null
}
```

