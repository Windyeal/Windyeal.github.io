---
layout:     post
title:      "HiDL中的PreExecute"
subtitle:   ""
date:       2025-04-05
author:     "Hisilcon"
header-style: text
catalog: true
published: true

tags:
    - HiCBB
    - SMT7
    
---
# PreExecute功能

用于在测试前添加向量鉴权、relay切换的动作，不支持单独Functional模式，支持Functional+Diag模式。

## PreExecute参数

**PreExecute**：选择是否启用向量鉴权和relay切换的功能，默认为OFF，ON为开启，开启时会显示相关UI界面。

**PreLabel_EN**：选择向量鉴权的使用位置，默认为OFF，可选ALL、Point、OFF。

OFF：代表不使用PreExectue功能。

ALL: 代表在测试项整体执行之前执行向量鉴权。

Point：代表在Shmoo、VminVmax、FminFmax、SramRetention、PinMargin模式每个点执行之前执行向量鉴权。

HiFuanctional模式和Functional+Diag模式只支持ALL，选择Point无效。Shmoo、VminVmax、FminFmax、PinMargin、SramRetention选ALL代表在整体扫描之前执行向量鉴权，选Point代表在扫描每个点之前执行向量鉴权。

**DFT_EN**：填入需要跑的第一条鉴权向量(不执行向量鉴权时，请将参数PreLabel_EN选为OFF)。

**DFT_SETUP**：填入需要跑的第二条鉴权向量(没有第二条鉴权向量时请为空，不要进行填写)。

**DFT_OTHER**：填入需要跑的第三条鉴权向量(没有第三条鉴权向量时请为空，不要进行填写)。

上面三个参数可以每个参数可填写一条鉴权向量，执行顺序为先执行DFT_EN，再执行DFT_SETUP，最后执行DFT_OTHER。

填写格式为:{pattern_name};{level_information};{timing_information}

注意：timing、pattern、level信息用“;”隔开timing和level的Equation、Spec、set用“,”隔开，timing如果时multiport格式的话直接copy Timing参数中Spec/Wave里mutiportspec的名称（注意copy时不要带“引号”）。

示例1：AUTH_R02_HI3670V100_x1_S_52ns_V1;4,1,1;99,1,1）

示例2：AUTH_R02_HI3670V100_x1_S_52ns_V1;4,1,1; CHAIN_R01_X1_M_40ns_P03_cb_Spec

**Relay_EN**：选择是否启用relay切换的动作，默认为OFF，可选Normal或Auto，对于HiDigitalLinkling代码来说选Normal或Auto没有区别，都会对relay进行操作。(测试项执行时realy操执最先执行，且只执行一次，单独Functional模式下开启PowerMonitor功能时，也支持PowerMonitor执行之前进行relay操作)

**RelayList_ON**：填入需要切换至ON的relay,默认为NA，NA表示无relay需要切换至ON。

**RelayList_OFF**：填入需要切换至OFF的relay，默认为NA，NA表示无relay需要切换至OFF。

**WaitingTimie(ms)**：填入鉴权向量执行之前的等待时间（单位：ms），默认为NA，NA代表无等待时间。(Functional+Diag模式下此参数无效)
