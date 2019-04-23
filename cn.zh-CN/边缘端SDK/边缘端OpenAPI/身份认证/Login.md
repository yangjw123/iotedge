# Login {#reference_gzj_mwl_jhb .reference}

POST /auth/login

## 功能描述 {#section_xwn_bvh_x2w .section}

用户登录网关认证的接口。调用该接口可获取接口返回的cookie，只有获取cookie后才能进行其他相关API的调用。

**说明：** 对其他所有接口的调用均需要携带本接口返回的cookie。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|UserName|String|是|登录网关的用户名。 **说明：** 网关的初始用户名为admin，密码为admin1234。可通过访问边缘网关控制台修改用户名密码和API访问权限。访问边缘网关控制台的操作请参考[远程服务访问](https://help.aliyun.com/document_detail/99135.html#h2-url-4)。

 |
|Password|String|是|用户名对应的密码。|

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code": 200,
        "message": "success",
        "data": {
            //UserName: 用户名
            "UserName": string
        }
    }
    ```

-   异常返回示例

    ```
    {
      "code": 400,
      "message": "Invalid username or password",
      "data": {
        "UserName": string
      }
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入:
curl -c "test_eweb.cookie" -d "{\"id\":111,\"version\":\"1.0\",\"request\":{\"apiVer\":\"0.6\"},\"params\":{\"UserName\": \"admin\", \"Password\": \"admin1234\"}}" -k -X POST https://127.0.0.1:9999/auth/login# 
# 输出:
{
    "code":200,
    "message":"success",
    "data":{
        "UserName":"admin"
    }
}
```

