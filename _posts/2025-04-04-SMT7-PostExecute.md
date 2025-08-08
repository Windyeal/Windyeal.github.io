---
layout:     post
title:      "HiDL中的PostExecute"
subtitle:   ""
date:       2025-04-04
author:     "Hisilcon"
header-style: text
catalog: true
published: true

tags:
    - HiCBB
    - SMT7
    
---
# PostExecute功能

用于在测试执行后再执行post向量或进行Reconnect操作，不支持单独Functional模式和Functional+Diag模式。

## PostExecute参数

**PostExecute**：选择是否启用执行Post向量功能或Reconnect功能，默认为OFF，ON为开启，开启时会显示相关UI界面。

**PostLabel_EN**：选择执行post向量的位置，默认为OFF，可选ALL、Point、OFF。

OFF：代表不使用PostExecute功能。

ALL: 代表在测试项整体执行之后执行Post向量。

Point：代表在Shmoo、VminVmax、SramRetention模式每个点执行之后执行所填向量。

HiFuanctional模式只支持ALL，选择Point无效。Shmoo、VminVmax、SramRetention选Point代表在每个点扫描之后执行所填的Post向量。
（<font color = Red>注意：FminFmax、PinMargin选Point时无效</font>）

**DFT_EN_Post**： 填入测试之后需要跑的第一条向量(不执行向量时，请将参数PostLabel_EN选为OFF)。

**DFT_SETUP_Post**： 填入测试之后需要跑的第二条向量(没有第二条向量时请为空，不要进行填写)。

**DFT_OTHER_Post**： 填入测试之后需要跑的第三条向量(没有第三条向量时请为空，不要进行填写)。

上面三个参数可以每个参数可填写一条向量，执行顺序为先执行DFT_EN_Post，再执行DFT_SETUP_Post，最后执行DFT_OTHER_Post。

该参数填写格式为:{pattern_name};{level_information};{timing_information}

注意：timing、pattern、level信息用“;”隔开timing和level的Equation、Spec、set用“,”隔开，timing如果时multiport格式的话直接copy Timing参数中Spec/Wave里mutiportspec的名称（注意copy时不要带“引号”）。

示例1：AUTH_R02_HI3670V100_x1_S_52ns_V1;4,1,1;99,1,1）

示例2：AUTH_R02_HI3670V100_x1_S_52ns_V1;4,1,1; CHAIN_R01_X1_M_40ns_P03_cb_Spec

**Enable**：
Reconnect中的Enable参数代表选择执行Reconnect操作的位置可选ALL、Point、OFF。

OFF：代表不使用PostExecute功能。

ALL: 代表在测试项整体执行之后执行Post向量。

Point：代表在Shmoo、VminVmax、SramRetention模式每个点执行之后执行Reconnect操作。

HiFuanctional模式只支持ALL，选择Point无效。Shmoo、VminVmax、SramRetention选Point代表在每个点扫描之后执行Reconnect操作量。
（<font color = Red>注意：FminFmax模式和PinMargin模式选Point时无效</font>）

**WaitingTime(ms)**：代表进行Reconnect操作时，Disconnect与Connect之间的时间间隔，默认为200（单位：ms）。
