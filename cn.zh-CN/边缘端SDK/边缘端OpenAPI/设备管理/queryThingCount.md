# queryThingCount {#reference_c5g_pwl_jhb .reference}

POST /thing/device/count

## 功能描述 {#section_xwn_bvh_x2w .section}

根据productKey获取设备的数量。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|productKey|String|否|设备所属产品的唯一标识符。可从物联网平台控制台获取。|
|activeStatus|Intger|否|设备的激活状态。取值如下： -   null：忽略状态
-   0：未激活
-   1：激活

 |
|onlineStatus|Intger|否|设备的在线状态。取值如下： -   null：忽略状态
-   0：离线
-   1：在线

 |

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "data": {"deviceCount": 30},
        "message": "success"
    }
    ```

-   异常返回示例

    ```
    {
      "code": 401,
      "data": null,
      "message": "resqust auth error"
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入
curl -b "test_eweb.cookie" -d "{\"request\":{ \"apiVer\": \"0.6\"}, \"params\": {}}" -k -X POST https://127.0.0.1:9999/thing/device/count
# 输出
{
    "code":200,
    "message":"success",
    "data":{
        "deviceCount":4
    }
}
```

