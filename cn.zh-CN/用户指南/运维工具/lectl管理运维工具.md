# lectl管理运维工具 {#concept_645162 .concept}

lectl管理运维工具（以下统称lectl）是物联网边缘计算提供的管理Link IoT Edge及其资源的命令行工具，可帮助您更好的使用Link IoT Edge。

您可以在\{LINKEDGE\_ROOT\}/gateway/build/bin目录下找到lectl工具。

**说明：** \{LINKEDGE\_ROOT\}指Link IoT Edge软件包根目录所在的路径，通常为/linkedge/。

## 获取帮助 {#section_r2u_b16_qz2 .section}

在`lectl`及子命令后添加--help命令，可获取帮助信息。顶层的帮助信息如下：

``` {#codeblock_x32_wl2_qcc}
$ lectl --help

Usage:  lectl [OPTIONS] COMMAND

Manage Link IoT Edge services and provide local services.

Options:
  -v, --version   Print version information and quit

Commands:
  completion  Output shell completion code
  config      Manage configs
  device      Manage devices
  diagnose    Check if the local environment is setup correctly
  fc          Manage function compute
  logger      Manage logger service and logs
  sc          Manage stream compute

Run 'lectl COMMAND --help' for more information on a command.
```

## 自动补全 {#section_cr3_rxj_t3e .section}

lectl支持bash和zsh的自动补全功能，提升输入效率。

 **bash** 

通过在网关上执行lectl completion bash命令，生成Lectl的bash自动补全脚本，并将脚本导入到Shell中，即可启动Lectl的bash自动补全功能功能。

但由于bash自动补全脚本依赖bash-completion，且各种包管理系统提供的bash-completion不同，因此您需要按照如下步骤启动Lectl的bash自动补全功能。

1.  在网关上执行type \_init\_completion命令，检查系统是否安装了bash自动补全脚本依赖的bash-completion。
    -   已安装：请跳转到步骤4。
    -   未安装：请跳转到步骤2。
2.  通过系统自带的包管理系统，安装bash-completion。

    -   RedHat系列操作系统：yum install bash-completion
    -   Debian系列操作系统：apt-get install bash-completion
    关于更多包管理系统提供的bash-completion相关信息，请参见[这里](https://github.com/scop/bash-completion#installation)。

3.  将安装bash-completion后生成的/usr/share/bash-completion/bash\_completion文件添加到.bashrc文件中。

    ``` {#codeblock_h4p_xes_trd}
    source /usr/share/bash-completion/bash_completion
    ```

4.  启用自动补全功能。

    有如下两种启用方法：

    -   直接导入bash自动补全脚本到当前的Shell。（推荐使用）

        ``` {#codeblock_61a_lk4_b8n}
        source <(lectl completion bash)
        ```

        **说明：** 使用此方法后，在退出Shell时自动补全功能失效。若需要自动补全功能一直生效，请执行echo 'source <\(lectl completion bash\)' \>\> ~/.bashrc，将此命令添加到.bashrc文件中。

    -   将bash自动补全脚本添加到bash\_completion.d目录。

        ``` {#codeblock_p6d_7mg_ge2}
        lectl completion bash > /etc/bash_completion.d/lectl
        ```


 **zsh** 

通过lectl completion zsh命令，生成Lectl的zsh自动补全脚本，并将生成的脚本导入到Shell中，即可启用zsh自动补全功能。

在网关上执行如下命令，一步实现生成zsh自动补全脚本和启用自动补全功能。

``` {#codeblock_s08_yc8_10g}
source <(lectl completion zsh)
```

**说明：** 如果出现`complete:13: command not found: compdef`错误，请将如下命令复制粘贴到.zshrc文件里：

``` {#codeblock_yox_zzw_hco}
autoload -Uz compinit
compinit
```

## 连接诊断 {#section_9v1_nyq_k0b .section}

当Link IoT Edge无法连接到云端时，您可以通过lectl工具，使用diagnose命令做初步诊断。

``` {#codeblock_0li_bsg_e7y}
lectl diagnose
```

系统显示类似如下信息：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/518977/156291705149255_zh-CN.png)

|字段|描述|
|--|--|
|Get Gateway Triple|获取网关设备的设备证书。|
|Get IoT Region|获取地域配置。|
|Check Network|检查网络连接状态。|
|Check DNS Service|检查DNS服务状态。|
|Check MQTT Port|检查MQTT协议端口。|
|Check MQTT Cert|检查MQTT协议证书。|
|Check MQTT Connection|检查MQTT连接。|

## 管理日志 {#section_knr_4en_tdt .section}

您可以使用lectl工具，打包日志或临时改变日志服务行为，方便在出问题时上传日志或临时排查。

-   **打包日志** 

    执行如下命令打包日志：

    ``` {#codeblock_njk_ryd_6oj}
    lectl logger pack
    ```

    **说明：** 日志文件被默认打包到当前目录并命名为logs.zip。您也可以通过-n或--name选项指定输出文件名，-o或--output选项指定输出路径。

-   **管理日志服务** 

    Lectl允许获取日志服务配置，并临时改变日志服务行为。例如，Link IoT Edge出现问题时可以调整全局日志等级到debug，以显示更多详细信息。

    获取日志服务配置和改变日志服务行为主要通过如下命令实现：

    ``` {#codeblock_u3z_k2d_c7p}
    lectl logger config [OPTIONS]
    ```

    **说明：** lectl logger config命令支持一次配置多个日志选项。

    |选项名称|描述|
    |----|--|
    |-d，--disable|关闭日志系统、日志等级、模块日志、模块日志等级、输出目标、显示格式等。不能一次关闭多项内容。|
    |-e，--enable|开启日志系统、日志等级、模块日志、模块日志等级、输出目标、显示格式等。不能一次开启多项内容。|
    |--show|显示所有配置或指定配置信息。此选项只能以`--show=`形式指定。 指定配置项包括：

     -   dir：日志文件路径
    -   level：全局日志等级
    -   module：模块日志配置
    -   format：日志显示格式
    -   target：日志输出目标
    -   size：日志文件大小
 |
    |-g，--single-file-mb|设置单个日志文件大小（单位为MB）。|
    |-t，--total-files-mb|设置总体日志文件大小（单位为MB）。|


## 管理配置 {#section_9ti_6di_cpb .section}

配置管理主要通过config子命令实现。

-   **获取配置** 

    使用如下命令获取配置：

    ``` {#codeblock_nqi_445_ilm}
    lectl config get [OPTIONS] [ARG]
    ```

    默认情况下，\[ARG\]作为待获取值的键，但也会因\[OPTIONS\]而变更。\[OPTIONS\]的有效选项如下表格所示。

    |选项名称|描述|
    |----|--|
    |-d，--d3|获取所有设备的设备证书信息，无\[ARG\]。|
    |-v，--driver|获取给定驱动的配置，\[ARG\]为驱动名。|
    |-g，--g3|获取网关设备的设备证书信息，无\[ARG\]。|
    |-r，--regexp|获取给定键正则表达式的值，\[ARG\]为键正则表达式。|
    |-t，--timestamp|获取给定时间戳的值，\[ARG\]为时间戳。|
    |-s，--tsl|获取给定产品的TSL，\[ARG\]为产品的Product Key。|

    常见示例如下：

    ``` {#codeblock_gtx_b2b_vlg}
    $ lectl config get foo
    $ lectl config get -g
    $ lectl config get -d
    $ lectl config get -s foo
    $ lectl config get -v foo
    $ lectl config get -r ^foo$
    $ lectl config get -t 1555483052
    ```

-   **设备配置** 

    使用如下命令获取设备配置：

    ``` {#codeblock_vf1_pyy_s7x}
    lectl config set [OPTIONS] [ARG...]
    ```

    默认情况下，\[ARG...\]表示ARG1、ARG2、ARG3，分别为键、值和时间戳（可选），但也会因\[OPTIONS\]而变更。\[OPTIONS\]的有效选项如下表格所示。

    |选项名称|描述|
    |----|--|
    |-d，--d3|设置设备证书信息，ARG1、ARG2和ARG3分别为Product Key、Device Name和Device Secret。|
    |-p，--d3f|从给定的文件读取并设置设备证书信息，ARG1为文件路径，无ARG2和ARG3。|
    |-v，--driver|设置驱动配置，ARG1，ARG2分别为驱动名和驱动配置，无ARG3。|
    |-f，--file|从给定的文件读取并设置键、值。ARG1，ARG2分别为键和文件路径，无ARG3。|
    |-g，--g3|设置网关的设备证书信息，ARG1、ARG2和ARG3分别为Product Key、Device Name和Device Secret。|
    |-s，--tsl|设置产品的TSL，ARG1，ARG2分别为产品的Product Key和TSL文件路径。|

    常见示例如下：

    ``` {#codeblock_c0h_gjx_yr0}
    $ lectl config set foo bar
    $ lectl config set foo bar 1555483052
    $ lectl config set -f foo /path/to/bar
    $ lectl config set -g foo bar baz
    $ lectl config set -d foo bar baz
    $ lectl config set -p /path/to/foo
    $ lectl config set -s foo /path/to/bar
    $ lectl config set -v foo bar
    ```

-   **移除配置** 

    使用如下命令移除配置：

    ``` {#codeblock_vnk_7rq_p1c}
    lectl config unset KEY
    ```

-   **获取匹配键** 

    config子命令支持通过正则表达式来获取匹配的键，方便您进一步获取配置内容。命令如下：

    ``` {#codeblock_chi_uw7_s75}
    lectl config keys REGEXP
    ```

-   **强制写入** 

    为确保配置操作执行成功，您可以强制配置，并保存数据到磁盘。命令如下：

    ``` {#codeblock_zkj_y3n_wfp}
    lectl config flush
    ```


## 管理设备 {#section_bb8_zzh_u30 .section}

您可以通过device子命令来管理Link IoT Edge的设备相关信息。

-   **显示信息** 

    当前设备的状态信息，可通过lectl device show命令查看。

    一个显示信息片段如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/518977/156291705250568_zh-CN.png)

    |选项名称|描述|
    |----|--|
    |LocalId|本地ID地址。|
    |DriverName|设备关联驱动的名称（标识）。|
    |LocalConnected|是否连接到边缘端。|
    |CloudConnected|是否连接到云端。|
    |Authorized|鉴权是否通过。|
    |Activated|设备状态是否为已激活。|
    |LastCallTime|上一次对设备进行操作的时间。|


## 管理函数计算 {#section_721_i68_smb .section}

可以通过lectl管理Link IoT Edge上的函数计算。包括显示信息、部署函数、移除函数、重置部署、调用函数、重启函数等。

-   **显示信息** 

    当函数运行异常时，可通过lectl fc show命令查看函数的运行状态及统计信息。

    一个显示信息片段如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/518977/156291705249266_zh-CN.png)

-   **部署函数** 

    使用如下命令部署一个或多个函数：

    ``` {#codeblock_niq_t0i_jc1}
    lectl fc deploy FILE
    ```

    其中，FILE的格式说明请参见\{LINKEDGE\_ROOT\}/gateway/build/bin/fc\_deploy.conf文件内容。

-   **移除函数** 

    使用如下命令移除一个或多个函数：

    ``` {#codeblock_kfu_461_v11}
    lectl fc rm FUNCTION [FUNCTION...]
    ```

    其中，\[FUNCTION...\]为函数ID，多个函数ID以空格间隔。

-   **重置部署** 

    使用如下命令重置部署：

    ``` {#codeblock_ui9_pmn_h7i}
    lectl fc reset
    ```

-   **调用函数** 

    使用如下命令调用一个函数：

    ``` {#codeblock_t0h_s7r_kl2}
    lectl fc invoke FILE
    ```

    其中，FILE的格式说明请参见\{LINKEDGE\_ROOT\}/gateway/build/bin/fc\_invoke.conf文件内容。

-   **重启函数** 

    使用如下命令重启一个或多个函数：

    ``` {#codeblock_d0t_yye_r35}
    lectl fc restart FILE
    ```

    其中，FILE的格式说明请参见\{LINKEDGE\_ROOT\}/gateway/build/bin/fc\_restart.conf文件内容。


## 管理流数据分析 {#section_4pv_kmw_905 .section}

您可以在Link IoT Edge专业版中使用lectl工具管理流数据分析。

-   **显示信息** 

    可通过lectl sc show命令查看当前系统流数据任务状态。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/518977/156291705349372_zh-CN.png)

    |选项名称|描述|
    |----|--|
    |ID|流数据任务ID。|
    |Name|流数据任务名称。|
    |Running|流数据任务是否正在运行。|
    |SQLPath|SQL语句文件路径。|
    |SQLMd5|SQL语句文件MD5值。|
    |LogPath|流数据任务日志路径。|
    |BlinkJobId|流数据任务在Blink中对应的任务ID。|

-   **启动流数据任务** 

    使用如下命令启动一个或多个流数据任务：

    ``` {#codeblock_qbo_am1_giw}
    lectl sc start STREAM [STREAM...]
    ```

    其中，\[STREAM...\]为流数据任务ID，多个流数据任务ID以空格间隔。

-   **停止流数据任务** 

    使用如下命令停止一个或多个流数据任务：

    ``` {#codeblock_8n9_jmt_z2h}
    lectl sc stop STREAM [STREAM...]
    ```

    其中，\[STREAM...\]为流数据任务ID，多个流数据任务ID以空格间隔。

-   **验证SQL** 

    将SQL语句保存到指定文件，并执行如下命令验证流数据任务的SQL语句是否正确：

    ``` {#codeblock_umh_nsp_dn0}
    lectl sc checksql FILE
    ```

    其中，FILE的格式说明请参见\{LINKEDGE\_ROOT\}/gateway/build/bin/fc\_restart.conf文件内容。


