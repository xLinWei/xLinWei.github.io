---
layout: post
tags: risc-v
---

# 模块与融合
by WeiLin, 2019.7.20

### 1. 模块化
计算机体系结构的传统方法是增量ISA，即新处理器不仅要实现新的ISA扩展，还需要实现过去的所有扩展。而**RISC-V是模块化的**，这点跟Tensilica Xtensa架构有点像。

Tensilica Processor的设计哲学是：**“Configure the Core and select only the features you needed”**。这种哲学用在RISC-V也大致正确，不同的是，**Xtensa是可配置的，而RISC-V是可设计的**。区别的原因在于两者的定位不同，Tensilica主要是用来为Cadence设计IP的，而RISC-V是用来设计自主CPU的。

**RISC-V将指令集划分为几个标准的子集，称为扩展**。并且这些扩展是可选的(基础扩展RV32I是必选的)，处理器的设计者可以根据需求选择实现不同的扩展。这种模块化特性使得RISC-V具有了袖珍化、低能耗的特点，而这对于嵌入式应用可能至关重要。 下表为RISC-V的部分指令集。

E | 描述
:-: | :-:
I   | 基础整数指令集RV32I，所有实现都必须支持。
M   | 整数乘除法扩展指令集RV32M
F/D | 单精度浮点、双精度浮点扩展RV32F/D
A   | 原子操作指令集RV32A，为同步操作提供了必要的支持。 
G   | 通用扩展(RV32G)为RISC-V基础整数指令集 RV32I加上标准扩展(M、F、D、A)，统称RV32G
C   | 压缩扩展(RV32C)为RISC-V的压缩指令集

### 2. 融合
“高端处理器可以通过将简单的指令组合在一起来提升性能，而不会因为更大、更复杂的ISA给低端实现带来负担。这种技术称为**宏观融合**，因为它将‘宏’指令综合在一起。”

也就是说，宏观融合通过组合简单指令实现复杂操作，而不是专门设计一个复杂ISA增加处理器设计难度。

例如："ARM-32具有一个不寻常的功能，对于大多数算术逻辑运算中的一个操作数，你可以选择对它进行移位。尽管这些指令的使用频率很低，但它使数据路径和数据通路更加复杂。与此相对的是，RV32I 提供了单独的移位指令。"

宏观融合是RISC-V保证简洁性的方法之一。
