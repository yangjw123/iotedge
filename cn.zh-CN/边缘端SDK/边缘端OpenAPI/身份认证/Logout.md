# Logout {#reference_l54_nwl_jhb .reference}

POST /auth/logout

## 功能描述 {#section_xwn_bvh_x2w .section}

用户登出网关的接口，一旦登出成功，当前session将无法继续调用API。

## 请求参数 {#section_a7p_44e_yn9 .section}

|参数名称|类型|是否必选|描述|
|:---|--|----|:-|
|UserName|String|是|登录网关时使用的用户名。 **说明：** 网关的初始用户名为admin，可通过访问边缘网关控制台修改用户名密码和API访问权限。访问边缘网关控制台的操作请参考[远程服务访问](https://help.aliyun.com/document_detail/99135.html#h2-url-4)。

 |

## 返回示例 {#section_vi4_ryb_i4q .section}

-   正常返回示例

    ```
    {
        "code":200,
        "message":"success",
        "data":{
        }
    }
    ```

-   异常返回示例

    ```
    {
        "code":400,
        "message":"cookie is invalid",
        "data":{
        }
    }
    ```


## 完整示例 {#section_ahy_n52_lhb .section}

```
# 输入:
curl -b "test_eweb.cookie" -d "{\"id\":111,\"version\":\"1.0\",\"request\":{\"apiVer\":\"0.6\"},\"params\":{\"UserName\": \"admin\"}}" -k -X POST https://127.0.0.1:9999/auth/logout# 
# 输出:
{
    "code":200,
    "message":"success",
    "data":{
    }
}
```

