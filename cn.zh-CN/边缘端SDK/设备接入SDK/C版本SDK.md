# C版本SDK {#concept_am2_t1s_xfb .concept}

本章为您介绍C版本的SDK使用方法及相关API。Link IoT Edge提供C版本的SDK，名称为linkedge-thing-access-sdk-c。C版本开源的SDK源码请见[开源C库](https://github.com/aliyun/link-iot-edge-access-sdk-c)。

## get\_properties\_callback {#section_n2l_rbs_xfb .section}

``` {#codeblock_346_csd_rfn}
/*
     * 获取属性（对应设备产品物模型属性定义）的回调函数, 需驱动开发者实现获取属性业务逻辑
     * 
     * LinkEdge 需要获取某个设备的属性时, SDK 会调用该接口间接获取到数据并封装成固定格式后回传给 LinkEdge.
     * 开发者需要根据设备id和属性名找到设备, 将获取到的属性值按照@device_data_t格式填充.
     *
     * @dev_handle:         LinkEdge 需要获取属性的具体某个设备.
     * @properties:         属性值键值结构, 驱动开发者需要将根据属性名称获取到的属性值更新到properties中.
     * @properties_count:   属性个数.
     * @usr_data:           注册设备时, 用户传递的私有数据.
     * 所有属性均获取成功则返回LE_SUCCESS, 其他则返回错误码(参考le_error.h错误码宏定义).
     * */
typedef int (*get_properties_callback)(device_handle_t dev_handle, 
                                       leda_device_data_t properties[], 
                                       int properties_count, 
                                       void *usr_data);
```

## set\_properties\_callback {#section_vhl_gcs_xfb .section}

``` {#codeblock_t1y_ejp_63c}
/*
     * 设置属性（对应设备产品物模型属性定义）的回调函数, 需驱动开发者实现设置属性业务逻辑
     * 
     * LinkEdge 需要设置某个设备的属性时, SDK 会调用该接口将具体的属性值传递给应用程序, 开发者需要在本回调
     * 函数里将属性设置到设备.
     *
     * @dev_handle:         LinkEdge 需要设置属性的具体某个设备.
     * @properties:         LinkEdge 需要设置的设备的属性名称和值.
     * @properties_count:   属性个数.
     * @usr_data:           注册设备时, 用户传递的私有数据.
     * 
     * 若获取成功则返回LE_SUCCESS, 失败则返回错误码(参考le_error.h错误码宏定义).
     * */
typedef int (*set_properties_callback)(device_handle_t dev_handle, 
                                       const leda_device_data_t properties[], 
                                       int properties_count, 
                                       void *usr_data);
```

## call\_service\_callback {#section_b4m_gcs_xfb .section}

``` {#codeblock_my1_698_q1z}
/*
     * 服务（对应设备产品物模型服务定义）调用的回调函数, 需要驱动开发者实现服务对应业务逻辑
     * 
     * LinkEdge 需要调用某个设备的服务时, SDK 会调用该接口将具体的服务参数传递给应用程序, 开发者需要在本回调
     * 函数里调用具体的服务, 并将服务返回值按照@device_data_t格式填充到output_data. 
     *
     * @dev_handle:   LinkEdge 需要调用服务的具体某个设备.
     * @service_name: LinkEdge 需要调用的设备的具体某个服务名, 名称与设备产品物模型一致.
     * @data:         LinkEdge 需要调用的设备的具体某个服务参数, 参数与设备产品物模型保持一致.
     * @data_count:   LinkEdge 需要调用的设备的具体某个服务参数个数.
     * @output_data:  开发者需要将服务调用的返回值, 按照设备产品物模型规定的服务格式返回到output中.
     * @usr_data:     注册设备时, 用户传递的私有数据.
     * 
     * 若获取成功则返回LE_SUCCESS, 失败则返回错误码(参考le_error.h错误码宏定义).
     * */
typedef int (*call_service_callback)(device_handle_t dev_handle, 
                                     const char *service_name, 
                                     const leda_device_data_t data[], 
                                     int data_count, 
                                     leda_device_data_t output_data[], 
                                     void *usr_data);
```

## leda\_report\_properties {#section_dzd_stb_6kf .section}

``` {#codeblock_vhg_n0b_ois}
/*
 * 上报属性, 在设备所属产品物模型中规定了设备的属性上报能力.
 *
 * 上报属性, 可以上报一个, 也可以多个一起上报.
 *
 * dev_handle:          设备在linkedge本地唯一标识.
 * properties:          @leda_device_data_t, 属性数组.
 * properties_count:    本次上报属性个数.
 *
 * 阻塞接口, 成功返回LE_SUCCESS,  失败返回错误码.
 *
 */
int leda_report_properties(device_handle_t dev_handle, const leda_device_data_t properties[], int properties_count);
```

## leda\_report\_event {#section_k7y_xru_2d5 .section}

``` {#codeblock_n20_cnp_2s4}
/*
 * 上报事件, 设备具有的事件上报能力在设备产品物模型有规定.
 *
 * 
 * dev_handle:  设备在linkedge本地唯一标识.
 * event_name:  事件名称.
 * data:        @leda_device_data_t, 事件参数数组.
 * data_count:  事件参数数组长度.
 *
 * 阻塞接口, 成功返回LE_SUCCESS,  失败返回错误码.
 *
 */
int leda_report_event(device_handle_t dev_handle, const char *event_name, const leda_device_data_t data[], int data_count);
```

## leda\_offline {#section_gaa_xve_6p2 .section}

``` {#codeblock_qke_6h7_wxe}
/*
 * 下线设备, 假如设备工作在不正常的状态或设备退出前, 可以先下线设备, 这样LinkEdge就不会继续下发消息到设备侧.
 *
 * dev_handle:  设备在linkedge本地唯一标识.
 *
 * 阻塞接口, 成功返回LE_SUCCESS,  失败返回错误码.
 *
 */
int leda_offline(device_handle_t dev_handle);
```

## leda\_online {#section_vyi_d6m_ay5 .section}

``` {#codeblock_m67_p9f_sps}
/*
 * 上线设备, 设备只有上线后, 才能被 LinkEdge 识别.
 *
 * dev_handle:  设备在linkedge本地唯一标识.
 *
 * 阻塞接口,成功返回LE_SUCCESS, 失败返回错误码.
 */
int leda_online(device_handle_t dev_handle);
```

## leda\_register\_and\_online\_by\_device\_name {#section_p5g_omo_4cz .section}

``` {#codeblock_uaq_53v_lej}
/*
 * 通过已在阿里云物联网平台创建的设备device_name, 注册并上线设备, 申请设备唯一标识符.
 *
 * 若需要注册多个设备, 则多次调用该接口即可.
 *
 * product_key: 在阿里云物联网平台创建的产品ProductKey.
 * device_name: 在阿里云物联网平台创建的设备名称DeviceName.
 * device_cb:   请求调用设备回调函数结构体，详细描述见@leda_device_callback.
 * usr_data:    设备注册时传入私有数据, 在回调中会传给设备.
 *
 * 阻塞接口, 返回值设备在linkedge本地唯一标识, >= 0表示有效, < 0 表示无效.
 *
 */
device_handle_t leda_register_and_online_by_device_name(const char *product_key, const char *device_name, leda_device_callback_t *device_cb, void *usr_data);
```

## leda\_register\_and\_online\_by\_local\_name {#section_735_ax9_qt3 .section}

``` {#codeblock_18f_zyq_iaq}
/*
 * 通过本地自定义设备名称, 注册并上线设备, 申请设备唯一标识符.
 *
 * 若需要注册多个设备, 则多次调用该接口即可.
 *
 * product_key: 在阿里云物联网平台创建的产品ProductKey.
 * local_name:  由设备特征值组成的唯一描述信息, 必须保证同一个product_key时，每个设备名称不同.
 * device_cb:   请求调用设备回调函数结构体，详细描述见@leda_device_callback.
 * usr_data:    设备注册时传入私有数据, 在回调中会传给设备.
 *
 * 阻塞接口, 返回值设备在linkedge本地唯一标识, >= 0表示有效, < 0 表示无效.
 *
 * 注: 在同一产品ProductKey条件设备注册, 不允许本接口和leda_register_and_online_by_device_name接口同时使用, 
 *     即每一个产品ProductKey设备注册必须使用同一接口, 否则设备注册会发生不可控行为.
 */
device_handle_t leda_register_and_online_by_local_name(const char *product_key, const char *local_name, leda_device_callback_t *device_cb, void *usr_data);
```

## leda\_init {#section_a3n_gcs_xfb .section}

``` {#codeblock_91a_db0_77f}
/*
 * 驱动模块初始化, 模块内部会创建工作线程池, 异步执行阿里云物联网平台下发的设备操作请求, 工作线程数目通过worker_thread_nums配置.
 *
 * worker_thread_nums : 线程池工作线程数, 该数值根据注册设备数量进行设置.
 *
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 */
int leda_init(int worker_thread_nums);
```

## leda\_exit {#section_e2r_sc0_7h7 .section}

``` {#codeblock_zty_p64_5ak}
/*
 * 驱动模块退出.
 *
 * 模块退出前, 释放资源.
 *
 * 阻塞接口.
 */
void leda_exit(void);
```

## leda\_get\_driver\_info\_size {#section_kmn_9oo_0j7 .section}

``` {#codeblock_ryi_6a8_hiw}
/*
 * 获取驱动信息长度.
 *
 * 阻塞接口, 成功返回驱动信息长度, 失败返回0.
 */
int leda_get_driver_info_size(void);
```

## leda\_get\_driver\_info {#section_gap_4py_gbh .section}

``` {#codeblock_5ue_boi_03s}
/*
 * 获取驱动信息(在物联网平台配置的驱动配置).
 *
 * driver_info: 驱动信息, 需要提前申请好内存传入.
 * size:          驱动信息长度, leda_get_driver_info_size, 如果传入driver_info比实际配置内容长度短, 会返回LE_ERROR_INVAILD_PARAM.
 *  
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 * 
 * 配置格式:
    {
        "json":{
            "ip":"127.0.0.1",
            "port":54321
        },
        "kv":[
            {
                "key":"ip",
                "value":"127.0.0.1",
                "note":"ip地址"
            },
            {
                "key":"port",
                "value":"54321",
                "note":"port端口"
            }
        ],
        "fileList":[
            {
                "path":"device_config.json"
            }
        ]
    }
 */
int leda_get_driver_info(char *driver_info, int size);
```

## leda\_get\_device\_info\_size {#section_nl7_k9y_48z .section}

``` {#codeblock_00r_nu0_rq2}
/*
 * 获取设备信息长度.
 *
 * 阻塞接口, 成功返回设备信息长度, 失败返回0.
 */
int leda_get_device_info_size(void);
```

## leda\_get\_device\_info {#section_qr1_8u1_hdh .section}

``` {#codeblock_bs7_7qp_m2r}
/*
 * 获取设备信息(在物联网平台配置的设备配置).
 *
 * device_info:  设备信息, 需要提前申请好内存传入.
 * size:         设备信息长度, 该长度通过leda_get_device_info_size接口获取, 如果传入device_info比实际配置内容长度短, 会返回LE_ERROR_INVAILD_PARAM.
 *  
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 * 
 * 配置格式:
    [
        {
            "custom":{
                "port":12345,
                "ip":"127.0.0.1"
            },
            "deviceName":"device1",
            "productKey":"a1ccxxeypky"
        }
    ]
 */
int leda_get_device_info(char *device_info, int size);
```

## leda\_get\_config\_size {#section_kze_fl2_bvu .section}

``` {#codeblock_2yq_7v0_v4m}
/*
 * 获取驱动配置长度.
 *
 * 阻塞接口, 成功返回驱动配置长度, 失败返回0.
 */
int leda_get_config_size(void);
```

## leda\_get\_config {#section_aav_fi0_kjj .section}

``` {#codeblock_phh_6ww_ini}
/*
 * 获取驱动所有配置.
 *
 * config:       驱动配置, 需要提前申请好内存传入.
 * size:         驱动配置长度, 该长度通过leda_get_config_size接口获取, 如果传入config比实际配置内容长度短, 会返回LE_ERROR_INVAILD_PARAM.
 *  
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 * 
 * 配置格式:
    {
        "config":{
            "json":{
                "ip":"127.0.0.1",
                "port":54321
            },
            "kv":[
                {
                    "key":"ip",
                    "value":"127.0.0.1",
                    "note":"ip地址"
                },
                {
                    "key":"port",
                    "value":"54321",
                    "note":"port端口"
                }
            ],
            "fileList":[
                {
                    "path":"device_config.json"
                }
            ]
        },
        "deviceList":[
            {
                "custom":"{"port":12345,"ip":"127.0.0.1"}",
                "deviceName":"device1",
                "productKey":"a1ccxxeypky"
            }
        ]
    }
 */
int leda_get_config(char *config, int size);
```

## config\_changed\_callback {#section_hzn_gcs_xfb .section}

``` {#codeblock_gh6_y14_qhr}
/*
 * 驱动配置变更回调接口.
 *
 * config:        配置信息.
 *
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 */
typedef int (*config_changed_callback)(const char *config);
```

## leda\_register\_config\_changed\_callback {#section_tq4_gcs_xfb .section}

``` {#codeblock_gwb_o1g_28a}
/*
 * 订阅驱动配置变更监听回调.
 *
 * config_cb:      配置变更通知回调接口.
 *
 * 阻塞接口, 成功返回LE_SUCCESS,失败返回错误码.
 */
int leda_register_config_changed_callback(config_changed_callback config_cb);
```

## leda\_get\_tsl\_size {#section_ml5_gcs_xfb .section}

``` {#codeblock_eqv_mo9_ago}
/*
 * 获取指定产品ProductKey对应物模型内容长度.
 *
 * product_key:   产品ProductKey.
 *
 * 阻塞接口, 成功返回product_key对应物模型内容长度, 失败返回0.
 */
int leda_get_tsl_size(const char *product_key);
```

## leda\_get\_tsl {#section_lcv_gcs_xfb .section}

``` {#codeblock_a0n_h8e_0mn}
/*
 * 获取指定产品ProductKey对应物模型内容.
 *
 * product_key:  产品ProductKey.
 * tsl:          物模型内容, 需要提前申请好内存传入.
 * size:         物模型内容长度, 该长度通过leda_get_tsl_size接口获取, 如果传入tsl比实际物模型内容长度短, 会返回LE_ERROR_INVAILD_PARAM.
 *  
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 */
int leda_get_tsl(const char *product_key, char *tsl, int size);
```

## leda\_get\_tsl\_ext\_info\_size {#section_p3q_nd1_3di .section}

``` {#codeblock_yjt_5zm_eu7}
/*
 * 获取指定产品ProductKey对应物模型扩展信息内容长度.
 *
 * product_key:   产品ProductKey.
 *
 * 阻塞接口, 成功返回product_key对应物模型扩展信息内容长度, 失败返回0.
 */
int leda_get_tsl_ext_info_size(const char *product_key);
```

## leda\_get\_tsl\_ext\_info {#section_eas_bee_eay .section}

``` {#codeblock_8wa_e60_cm1}
/*
 * 获取指定产品ProductKey对应物模型扩展信息内容.
 *
 * product_key:  产品ProductKey.
 * tsl_ext_info: 物模型扩展信息, 需要提前申请好内存传入.
 * size:         物模型扩展信息长度, 该长度通过leda_get_tsl_ext_info_size接口获取, 如果传入tsl_ext_info比实际物模型扩展信息内容长度短, 会返回LE_ERROR_INVAILD_PARAM.
 *  
 * 阻塞接口, 成功返回LE_SUCCESS, 失败返回错误码.
 */
int leda_get_tsl_ext_info(const char *product_key, char *tsl_ext_info, int size);
```

## leda\_get\_device\_handle {#section_g1y_gcs_xfb .section}

``` {#codeblock_eca_y66_onl}
/*
 * 获取设备句柄.
 *
 * product_key: 产品ProductKey.
 * device_name: 设备名称DeviceName.
 *
 * 阻塞接口, 成功返回device_handle_t, 失败返回小于0数值.
 */
device_handle_t leda_get_device_handle(const char *product_key, const char *device_name);
```

