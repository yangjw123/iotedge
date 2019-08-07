# Nodejs版本SDK {#concept_ycs_pcp_32b .concept}

设备接入SDK用于您在网关上开发驱动，将设备连接到网关，进而连接到物联网平台。

Node.js版本开源的SDK源码请见[开源的Node.js库](https://github.com/aliyun/linkedge-thing-access-sdk-nodejs)。

## 安装和使用 {#section_p2z_rvz_bhb .section}

1.  您可以通过如下命令来安装SDK：

    ``` {#codeblock_ka6_8tw_mw1}
    npm install linkedge-thing-access-sdk
    ```

    **说明：** 您也可以通过物联网边缘计算提供的[开发工具](../../../../cn.zh-CN/用户指南/函数计算/开发工具/更多用法.md#)使用该SDK来开发驱动。

2.  安装完成后，您可以根据SDK接口进行驱动开发。

    **说明：** 完成驱动开发后，直接运行会提示错误，必须通过物联网平台控制台，将已开发的驱动部署到网关中方可执行。部署驱动到网关的操作请参考[驱动开发](../../../../cn.zh-CN/用户指南/设备接入/驱动开发/概览.md#)。

    使用SDK开发驱动的示例代码片段如下所示：

    ``` {#codeblock_i8e_bat_gsy}
    const {
      Config,
      ThingAccessClient
    } = require('linkedge-thing-access-sdk');
    
    const callbacks = {
      setProperties: function (properties) {
        // Set properties to the physical thing and return the result.
        // Return an object representing the result or the promise wrapper of the object.
        return {
          code: 0,
          message: 'success',
          }
        };
      },
      getProperties: function (keys) {
        // Get properties from the physical thing and return the result.
        // Return an object representing the result or the promise wrapper of the object.
        return {
          code: 0,
          message: 'success',
          params: {
            key1: 'value1',
            key2: 'value2',
          }
        };
      },
      callService: function (name, args) {
        // Call services on the physical thing and return the result.
        // Return an object representing the result or the promise wrapper of the object.
        return new Promise((resolve) => {
          resolve({
            code: 0,
            message: 'success',
          });
        });
      }
    };
    Config.get()
      .then(config => {
        const thingInfos = config.getThingInfos();
        thingInfos.forEach(thingInfo => {
          const client = new ThingAccessClient(thingInfo, callbacks);
          client.registerAndOnline()
            .then(() => {
              return new Promise(() => {
                setInterval(() => {
                  client.reportEvent('high_temperature', { temperature: 41 });
                  client.reportProperties({ 'temperature': 41 });
                }, 2000);
              });
            })
            .catch(err => {
              console.log(err);
              client.cleanup();
            });
            .catch(err => {
              console.log(err);
            });
        });
      });
    ```


## 常量定义 {#section_cjg_v4g_chb .section}

|名称|类型|描述|
|--|--|--|
|PRODUCT\_KEY|String|配置对象（传给ThingAccessClient构造函数）的键值，指定云端分配的productKey。|
|DEVICE\_NAME|String|配置对象（传给ThingAccessClient构造函数）的键值，指定云端分配的deviceName。|
|LOCAL\_NAME|String|配置对象（传给ThingAccessClient构造函数）的键值，指定本地自定义的设备名。|
|CALL\_SERVICE|String|回调对象（传给ThingAccessClient构造函数）的键值，指定调用设备服务回调函数。回调函数格式请参见callbacks.callService\(\)。|
|GET\_PROPERTIES|String|回调对象（传给ThingAccessClient构造函数）的键值，指定获取设备属性回调函数。回调函数格式请参见callbacks.getProperties\(\)。|
|SET\_PROPERTIES|String|回调对象（传给ThingAccessClient构造函数）的键值，指定设置设备属性回调函数。回调函数格式请参见callbacks.setProperties\(\)。|
|RESULT\_SUCCESS|Number|操作成功。用于回调函数返回状态码。|
|RESULT\_FAILURE|Number|操作失败。用于回调函数返回状态码。|
|ERROR\_CLEANUP|String|调用cleanup\(\)出错错误码。|
|ERROR\_CONNECT|String|调用registerAndOnline\(\)出错错误码。|
|ERROR\_DISCONNECT|String|调用offline\(\)出错错误码。|
|ERROR\_GET\_CONFIG|String|调用getConfig\(\)出错错误码。|
|ERROR\_GET\_TSL|String|调用getTsl\(\)出错错误码。|
|ERROR\_GET\_TSL\_EXT\_INFO|String|调用getTslExtInfo\(\)出错错误码。|
|ERROR\_UNREGISTER|String|调用unregister\(\)出错错误码。|

## Config {#section_az2_wdh_chb .section}

驱动相关配置信息。

**static get\(\)**

返回全局的驱动配置对象，该配置通常在设备与驱动程序关联时由系统自动生成。该接口与getConfig\(\)的区别在于前者返回配置对象，后者返回配置字符串。

**说明：** 该接口的Config.get\(\)调用方法与getConfig\(\)接口的区别在于，getConfig\(\)返回配置字符串，Config.get\(\)返回配置对象。

返回值：

``` {#codeblock_zxa_zls_v7b}
Promise<Config>
```

**static registerChangedCallback\(callback\)**

注册配置变更回调函数

|名称|类型|描述|
|--|--|--|
|callback\(String\)|Function|回调函数，配置变更时被调用。|

**static unregisterChangedCallback\(callback\)**

注销配置变更回调函数。

|名称|类型|描述|
|--|--|--|
|callback\(String\)|Function|回调函数，配置变更时被调用。|

**Config\(string\)**

基于配置字符串构造新的Config对象。

|名称|类型|描述|
|--|--|--|
|string|String|JSON配置字符串。|

**getThingInfos\(\)**

返回所有设备相关信息。

返回值：

``` {#codeblock_tz9_0ig_clz}
ThingInfo[]
```

 **getDriverInfo\(\)** 

返回驱动相关信息。

返回值：

``` {#codeblock_f4a_21l_3fh}
Object
```

## ThingInfo {#section_e2d_pdh_chb .section}

此类接口是用于连接Link IoT Edge的设备信息的封装。

**ThingInfo\(productKey, deviceName, custom\)**

构造一个新的ThingInfo对象。

|名称|类型|描述|
|--|--|--|
|productKey|String|产品唯一标识。|
|deviceName|String|设备名称。|
|custom|Object|设备自定义配置。|

## ThingAccessClient {#section_rh3_twf_chb .section}

设备接入客户端，您可以通过该客户端来主动上报设备属性或事件，也可被动接受云端下发的指令。

**ThingAccessClient\(config, callbacks\)**

构造函数，使用指定的config和callbacks构造。

|名称|类型|描述|
|--|--|--|
|config|Object|元数据，用于配置该客户端。取值格式为： ``` {#codeblock_ckt_olb_q3p}
{
    "productKey": "Your Product Key", 
    "deviceName": "Your Device Name"
}
```

 |
|callbacks|Object|回调函数对象。取值格式为： ``` {#codeblock_zs7_fbh_3iv}
callbacks: {
    setProperties: function(properties) {},
    getProperties: function(keys) {},
    callService: function(name, args) {}
}
```

 -   指定设置设备属性的回调参数，请参见本文下方callbacks.setProperties内容
-   指定获取设备属性的回调参数，请参见本文下方callbacks.getProperties内容
-   指定调用设备服务的回调参数，请参见本文下方callbacks.callService内容

 |

**callbacks.setProperties\(properties\)**

设置具体设备属性的回调函数。通过回调函数，实现设置设备的属性。

|名称|类型|描述|
|--|--|--|
|properties|Object|设置属性的对象，取值格式为： ``` {#codeblock_zad_9ii_jo4}
{
    "key1": "value1", 
    "key2": "value2"
}
```

 |

返回值：

``` {#codeblock_o9s_61w_a01}
{
  "code": 0,
  "message": "string",
  "params": {}
}
```

|名称|类型|描述|
|--|--|--|
|code|Number|状态码。 -   0：接口调用成功。
-   非0：接口调用失败，报非0值对应的错误。

 |
|message|String|可选参数，状态描述信息。|
|params|Object|可选参数，用于返回每个属性的设置结果，其值为每个属性设置后的实际值。|

**callbacks.getProperties\(keys\)**

获取具体设备属性的回调函数。通过回调函数，实现获取设备的属性。

|名称|类型|描述|
|--|--|--|
|keys|String\[\]|获取属性对应的名称，取值格式为： ``` {#codeblock_zvp_cc0_a1m}
['key1', 'key2']
```

 |

返回值：

``` {#codeblock_pzs_wfr_5ef}
{
  "code": 0,
  "message": "string",
  "params": {}
}
```

|名称|类型|描述|
|--|--|--|
|code|Number|状态码。 -   0：接口调用成功。
-   非0：接口调用失败，报非0值对应的错误。

 |
|message|String|可选参数，状态描述信息。|
|params|Object|可选参数，用于获取属性成功时，返回对应的属性值。|

**callbacks.callService\(name, args\)**

调用设备服务回调函数。通过回调函数，实现调动设备服务。

|名称|类型|描述|
|--|--|--|
|name|String|设备服务名称。|
|args|Object|服务入参列表，取值格式为： ``` {#codeblock_s2d_kmn_9a5}
{
    "key1": "value1", 
    "key2": "value2"
}
```

 |

|名称|类型|描述|
|--|--|--|
|code|Number|状态码。 -   0：接口调用成功。
-   非0：接口调用失败，报非0值对应的错误。

 |
|message|String|可选参数，状态描述信息。|
|params|Object|可选参数，用于调用设备服务成功时，返回额外的信息。|

**setup\(\)**

设备接入客户端初始化。

**说明：** Link IoT Edge当前版本已不再使用该接口，之前遗留的调用不受影响。

返回值：

``` {#codeblock_ho6_6x7_y61}
Promise<Void>
```

**registerAndOnline\(\)**

将设备注册到网关中并通知网关上线设备。设备需要注册并上线后，设备端才能收到云端下发的指令或者发送数据到云端。

返回值：

``` {#codeblock_e0k_iq7_zmy}
Promise<Void>
```

**online\(\)**

通知网关设备已上线，该接口一般在设备离线后再次上线时使用。

返回值：

``` {#codeblock_r57_gu8_l8n}
Promise<Void>
```

**offline\(\)**

通知网关设备已离线。

返回值：

``` {#codeblock_3x2_nj7_9vr}
Promise<Void>
```

**reportEvent\(eventName, args\)**

主动上报设备事件。

|名称|类型|描述|
|--|--|--|
|eventName|String|事件对应的名称，与您在产品定义中创建事件的名称一致。|
|args|Object|事件中包含的属性key与value，取值格式为： ``` {#codeblock_g3q_3zm_osa}
{
    "key1": "value1", 
    "key2": "value2"
}
```

 |

**reportProperties\(properties\)**

主动上报设备属性。

|名称|类型|描述|
|--|--|--|
|properties|Object|属性中包含的属性key与value，取值格式为： ``` {#codeblock_h35_x9q_z2v}
{
    "key1": "value1", 
    "key2": "value2"
}
```

 |

**getTsl\(\)**

返回TSL字符串，数据格式与云端一致。

返回值：

``` {#codeblock_qo9_ig1_w7x}
Promise<Void>
```

 **getTslConfig\(\)** 

**说明：** Link IoT Edge当前版本已不再使用该接口，已使用getTslExtInfo\(\)接口代替，之前遗留的调用不受影响。

返回TSL配置字符串。

返回值：

``` {#codeblock_76l_83h_9o7}
Promise<String>
```

**getTslExtInfo\(\)**

返回TSL扩展信息字符串。

返回值：

``` {#codeblock_b45_a4u_z0d}
Promise<String>
```

**cleanup\(\)**

资源回收接口，您可以使用该接口回收您的资源。

返回值：

``` {#codeblock_uy1_1wq_2o5}
Promise<Void>
```

**unregister\(\)**

从网关中移除设备。请谨慎使用该接口。

返回值：

``` {#codeblock_ew1_m86_1ji}
Promise<Void>
```

## getConfig\(\) {#section_nmq_stg_chb .section}

获取驱动配置字符串，该配置通常在设备与驱动程序关联时由系统自动生成。

**说明：** 该接口与static get\(\)接口Config.get\(\)调用方法的区别在于getConfig\(\)返回配置字符串，Config.get\(\)返回配置对象。

返回值：

``` {#codeblock_j2q_1dt_q9f}
Promise<String>
```

## destroy\(\) {#section_pxq_ljz_3hb .section}

销毁库内部所有资源。通常不再使用此库时调用destroy\(\)接口。

返回值：

``` {#codeblock_rs8_82a_59y}
Promise<Void>
```

