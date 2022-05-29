---
title: Chapter 4
date: "2022-05-17"
description: "普通化学"
---

## 热力学第一定律

- 体系：指研究的对象，包含一定种类和数量的物质

- 环境：在体系之外，与体系密切相关的部分

- 体系分类

  - 敞开体系：能量+物质
  - 封闭体系：能量
  - 孤立体系：无交换

- 状态：体系所有物理性质和化学性质的综合表现

  - 始态
  - 终态

- 状态函数

  - 内能U、焓H、熵S、自由能G
  - 广延性质：有加和性
  - 强度性质：与物质的量无关

- 过程与途径

  - 过程：体系的状态随时间发生变化
  - 途径：体系变化过程中具体经历的状态

- 热力学第一定律：能量守恒定律

  $\Delta U = q + w$，w-功（+：环境->体系），q-热（+：环境->体系）

- 体积功的计算
  - 膨胀功：$w=-F\cdot \Delta L=-P_{外}\Delta V$
  - 可逆过程和最大功
    - $dw=-P_{外}\times dv\approx -P_{体}\times dv$
    - $w = -\int (nRT/V) dV = -nRTln(V_2/V_1) = -nRTln(P_1/P_2)$
  - 压缩功（压缩次数越多，环境对体系做功越小）
    - $dw=-P_{体}\cdot dv$
    - $w = -\int (nRT/V) dV = -nRTln(V_2/V_1) = -nRTln(P_1/P_2)$

<img src="img/1.JPG"  />

- 可逆过程
  - 相变点发生相变

## 热化学

- 恒容热效应
  - $V=C$, $dV=0$
  - $\Delta U=q_V$
- 恒压热效应
  - $P_{体}=P_{外}=C, dP=0$
  - $\Delta U=q_{P}+w_{P}=q_{P}-\int^{V_2}_{V_1}P_{外}dV$
  - $q_P = \Delta U + P_{外}(V_2-V_1) = \Delta (U+PV)$
- 焓与焓变
  - 定义：$U+PV=H$
  - $\Delta H=q_P$
  - 如果只有固态和液态的反应，$\Delta(PV)$较小，$\Delta H=\Delta U+\Delta (PV)=\Delta U$
  - $\Delta(PV)=\Delta nRT$
- 热容
  - $C = q/(T_2-T_1)$
  - 比热容：$c=C/m$，摩尔热容：$C_m=C/n$
  - $C_{V, m}$：摩尔恒容热容，$C_{p, m}$：摩尔恒压热容
  - 单原子分子理想气体：$C_{V, m}=3/2 R$，$C_{p, m}=5/2 R$
  - 双原子分子理想气体：$C_{V, m}=5/2 R$，$C_{p, m}=7/2R$
  - $\Delta H=C_p \Delta T$，$\Delta U=C_V \Delta T$
- 盖斯定律
  - $\Delta_f H_m^\theta = \sum n_i \Delta_f H_{m, 生成物i}^\theta - \sum n_j\Delta_f H^\theta_{m, 反应物j}$

