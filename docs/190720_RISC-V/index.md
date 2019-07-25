---
layout: post
tags: risc-v
---

# RISC-V
by WeiLin, 2019.7.18

之前上过一门课:“Nand2Tetris:从与非门到俄罗斯方块”，这门课是用一种简化的HDL语言设计一种非常简单的计算机(HACK Computer)，所以很好奇真正的计算机或者说处理器是怎么设计的。

后来了解了RISC-V，一种开源的ISA，进而知道了有很多基于RISC-V的开源处理器，所以开始自学RISC-V。

这里对RISC-V进行简单概括，大多是自己的整理和归纳，主要参考两本书：“The RISC-V Reader:An Open Architecture Atlas”和“手把手教你设计CPU——RISC-V处理器”。前一本是David Patterson与Andrew Waterman编写的RISC-V手册，有中文翻译版，而后一本是介绍开源蜂鸟E203 RISC-V处理器核。

### Content

[1. 模块与融合](./risc01.html)
：模块化/宏观融合

[2. 成本和性能](./risc02.html)
：成本因素/性能公式

[3. RV32I:基础指令集](./risc03.html)
：RV32I特性/寄存器组

[4. RV32I:Load/Store指令](./risc04.html)
：load/store/fence指令/存储器模型

[5. RV32I:分支指令](./risc05.html)
：条件跳转/条件码/延时槽/无条件跳转/函数调用
