# CredentialProviderChain {#reference_mms_3tz_3hb .reference}

调用该接口获取云服务访问凭据。

## CredentialProviderChain\(\).resolvePromise\(\) {#section_fhl_1gj_wgb .section}

该接口返回一个Promise对象，通过该返回内容获取访问云服务的临时凭据，凭据会定期更新（默认为15分钟）。因此当有访问云服务请求时，请调用该接口更新凭据。凭据格式参数如下：

|参数|类型|描述|
|:-|:-|:-|
|accessKeyId|String|访问密钥标识。访问密钥由AccessKeyID和AccessKeySecret组成，用于云服务API请求的身份认证。|
|accessKeySecret|String|访问密钥。|
|securityToken|String|安全令牌。|

## 调用示例 {#section_ucp_5gj_wgb .section}

本文以访问OSS云服务为例，描述CredentialProviderChain\(\).resolvePromise\(\)的用法。示例代码如下：

**说明：** 示例代码的详细解读可以参考[阿里云OSS服务访问](../../../../cn.zh-CN/用户指南/函数计算/应用场景/阿里云OSS服务访问.md#)。

```
'use strict';

var leSdk = require('linkedge-core-sdk');
var credChain= new leSdk.CredentialProviderChain();
var OSS = require('./node_modules/ali-oss');

exports.handler = function (event, context, callback) {
  // Retrieves group role credential.
  credChain.resolvePromise()
    .then((cred) => {
      console.log('Access Key Id: %s, Access Key Secret: %s, Security Token: %s',
        cred.accessKeyId, cred.accessKeySecret, cred.securityToken);

      // Constructs a client to interact with OSS cloud service.
      var client = new OSS({
        accessKeyId: cred.accessKeyId,
        accessKeySecret: cred.accessKeySecret,
        stsToken: cred.securityToken,
        region: 'oss-cn-shanghai',
        bucket: 'le-fc-bucket',
      });

      /* Upload local file to cloud. */
      return client.put('fileFromEdge.txt', "/linkedge/run/localFile.txt");
    })
    .then((result) => {
      console.log(result);
      callback(null);
    })
    .catch((err) => {
      console.log(err);
      callback(err);
    });
};
```

