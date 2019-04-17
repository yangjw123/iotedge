# CredentialProviderChain {#reference_mms_3tz_3hb .reference}

调用该接口获取云服务访问凭据。

## CredentialProviderChain\(\).get\_credential\(\) {#section_fhl_1gj_wgb .section}

该接口返回被访问云服务的临时凭据，凭据会定期更新（默认为15分钟）。因此当需要访问云服务时，请调用该接口更新凭据。凭据格式参数如下：

|参数|类型|描述|
|:-|:-|:-|
|accessKeyId|String|访问密钥标识。访问密钥由AccessKeyID和AccessKeySecret组成，用于云服务API请求的身份认证。|
|accessKeySecret|String|访问密钥。|
|securityToken|String|安全令牌。|

## 调用示例 {#section_ucp_5gj_wgb .section}

本文以访问OSS云服务为例，描述CredentialProviderChain\(\).get\_credential\(\)的用法。示例代码如下：

**说明：** 示例代码中依赖了第三方库oss2，可下载完整代码包[putOssFilePy-code.zip](http://link-iot-edge-packet.oss-cn-shanghai.aliyuncs.com/fc-demo/putOssFilePy-code.zip)，查看完整的代码。

```
# -*- coding: utf-8 -*-
import oss2
import lecoresdk

def handler(event, context):
  cred = lecoresdk.CredentialProviderChain().get_credential()
  auth = oss2.StsAuth(cred['accessKeyId'], cred['accessKeySecret'], cred['securityToken'])
  bucket = oss2.Bucket(auth, 'http://oss-cn-shanghai.aliyuncs.com', 'le-fc-bucket')
  bucket.put_object('fileFromEdgePy.txt', 'Content of object')
  print("-- Put fileFromEdgePy.txt to OSS.")
  return 'OK'
```

