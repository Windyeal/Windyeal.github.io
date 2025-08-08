---
layout:     post
title:      "HiDL中的VminVmax"
subtitle:   ""
date:       2025-04-02
author:     "Hisilcon"
header-style: text
catalog: true
published: true

tags:
    - HiCBB
    - SMT7
    
---
# VminVmax

## 模式介绍

进行改变电压范围，扫描出device的当前工作最大和最小电压测试。

使用场景：多用于可靠性测试，向量裕量测试，release前的数据收集（IP类,CHAIN,SCAN,MBIST测试项）

## 参数说明

**VminVmax**：填入Vmm的扫描方式，默认为MostSearch，可选MostSearch、BoundarySearch。
**Vcoef**：填入扫描的level spec name，默认为Vcoef。
**SpecType**：选择扫描点的计算方式RelativeMode、AbsoluteMode、RelativeCoefMode， 默认为RelativeMode。
**Vcoef_End**：填入扫描的终止点，默认为1.2。
**Vcoef_Start**：填入扫描的起始点，默认为0.6。
**V_points**：填入初次扫描时需要扫描的点数，默认为11。
**V_detail_points**：填入细扫时需要扫描的点数，默认为11，如果初次扫描没有边界点则不会细扫。
**Vclamp_EN**：选择ON或OFF,默认为ON，使用Vclamp时选择为ON，否则选择OFF。
**Output**：选择log输出模式，默认为File+ReportUI，可选File、ReportUI、File+ReportUI、None。
**PowerMonitor**：选择ON或OFF，默认为OFF，使用PowerMonitor功能时选择ON，否则选择OFF。
**PreExecute**：选择ON或OFF，默认为OFF，使用PreExecute功能时选择ON，否则选择OFF。
**LogFile**：填入log文件的路径和文件名，默认为“report/hidigitallink_log”。

## 参数解释

**MostSearch和BoundarySearch说明**：
用户在填入 MostSearch 时 电压扫描由起始点 Vcoef_ Start 开始到终止点 Vcoef_ End 结
束，记录 粗扫 pa ss 区间最长 的电压范围 ，若有相同长的 pass 区间取最右边的 pass 区间 ，程序将在该电压范围的最小电压值处进入 Vmin 的 detail 扫描 在该电压范围的最大电压值处进入 Vmax 的 detail 扫描填入 Boundary Search 时， 电压扫描由起始点 Vcoef_ Start 开始到终止点 Vcoef_ End 结束，程序将在扫描范围中所有 pass 点的最小电压值处进入 Vmin 的 detail 扫描；在扫描 范围中所有 pass 点的最大电压值处进入 Vmax 的 detail 扫描。

**RelativeMode和Absolute说明**:
RelativeMode模式下，Vcoef_Start和Vcoef_End代表扫描的起始扫描系数和终止扫描系数，各个point的扫描系数由Vcoef_Start和Vcoef_End均等分计算得出，<font color = Red>各个point的值为spec值乘当前point的扫描系数</font>。
AbsoluteMode模式下，Vcoef_Start和Vcoef_End代表扫描的起始值和终止值，<font color = Red>各个point的值Vcoef_Start和Vcoef_End均等分计算得出</font>。

**RelativeCoefMode说明**:
RelativeCoefMode模式下，对于硬件的执行和Relative模式一样，只是在处理结果时，将对于指定spec的VMM图以及相应的Vmin和Vmax由原来的电压值改为了比例系数。此模式可方便直接根据VminVmax确认当前电压下是否能pass。

**参数Vclamp_EN**：Vclamp_EN用于在VminVmax扫描过程中保护电路，参数为ON时保护生效，系统内部会检查当前所扫spec基于扫描之前初始值的变化，如果小于初始值的0.5倍(含0.5)或者大于初始值的1.5倍(含1.5)系统会报错停止VminVmax扫描，<font color = Red>非特殊情况，使用时请开启Vclamp_EN</font>。

## 细扫算法说明
HDL对于VminVmax、FminFmax、SramRetention测试，粗扫完成后会基于粗扫结果Margin点向pass区域多扫0.2个粗扫step，向fail区域多扫1.2个粗扫step，以更合理的抓取pass和fail的临界点。实际项目中粗扫的Margin点为第二个点或倒数第二个点时，向fail的区域扫1.2个粗扫step时扫描点的值会超过用户设置的start或end的值，因此我们优化了这部分的算法，如果超过用户设置的边界值时让其等于边界值。

## 注意事项

**EDL/STDF数据改动**
1.9.2版本之前的VminVmax功能在EDL/STDF中只写入Vmin、Vmax和其对应的值，从1.9.2版本开始，VminVmax的EDL/STDF中会打印SpecName、Vmin、Vmax、VMM_SpecType及其对应的值。
Vcoef为当前测试项Search的SpecName，后面显示的值是当前Spec的PrimaryValue
VMM_SpecType为固定字段，其值0代表当前测试项使用的是VMM的RelativeMode、1代表当前测试项用的是VMM的AbsoluteMode、2代表当前测试项用的是VMM的RelativeCoefMode
使用VMM的RelativeCoefMode时，上图中Vmin和Vmax的值代表是search的是系数值(并非实际电压值)

**参数Vclamp_EN**: Vclamp_EN关闭时需要注意拉偏电压，防止电压过大将芯片击穿。

**手动调试VminVmax模块时注意事项**：
为了防止Autorun时在Vmin扫描过程中出现异常(没有restore)而导致后面的测试项以及芯片所扫描的值都出现偏移，我们在1.8.1版本的VminVmax功能中增加了防呆，第一次run VminVmax之前会获取当前所扫描 Level Equation中当前 spec里所扫描变量的值并作为初始值保存好。在后续的扫描中相同Level Equation spec 的初始值都会使用该值，防止某个测试项异常没restore之前的值而影响后面的测试项和芯片的扫描范围。

增加此防呆后对于用户调试来说需要注意:
用户在调试过程中如果之前已经扫了某个spec的VminVmax，后面修改该spec值后runVminVmax，需要在run之前点击Terminate Test Method Execution 清除之前的存的值。

