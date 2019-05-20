---
layout: post
tags: computer
---

# Nand2Tetris

Nand2Tetris(从与非门到俄罗斯方块)是一个基于项目的课程，其全称为“依据基本原理构建现代计算机：从与非门到俄罗斯方块”。该课程从一个与非门(Nand)开始，根据设计好的指令系统，构建一个完整的计算机(_HACK Computer_)，并编写汇编器及编译器，最终实现Tetris游戏。

Nand2Tetris分成两门课，观课地址如下：  

- **Part1:** https://www.coursera.org/learn/build-a-computer  
- **Part2:** https://www.coursera.org/learn/nand2tetris2  

Part1的主要内容是构建 _HACK Computer_，并完成汇编器的编写；Part2是在 _HACK Computer_ 的基础上编写编译器，并设计Tetris游戏。

关于Part1的项目代码我放在了[这里](https://github.com/xLinWei/Nand2Tetris)，欢迎参考。

### Why Nand?

任意组合逻辑均可以表示成“与或非”的组合，这是因为最小表达式中就只有“与或非”。与非门和或非门又称作通用逻辑门，所有门均可以用**与非门、或非门**表示，在实际中一般使用与非门:
```
~ x = nand(x, x)
x & y = ~(nand(x, y))
x | y = ~( ~x & ~y )    //德摩根定理
```
_**那么为什么是与非门，而不是与门？**_ 这是因为静态CMOS门电路只能构造反相逻辑，像与非、或非，其它非反相逻辑需要多级CMOS门。_**那么为什么是与非门，而不是或非门？**_ 这是因为在相同面积下与非门的速度更快。
<br/><br/>

_**感想**_：所以无论多么复杂的结构，其实都可以用最简单的基本门来搭建。这门课的项目其实并不是很难(虽然名字听起来很高大上)，只不过需要花费较多的时间去做课下作业。相信听完这门课会对计算机有更清晰的认识。Part2是关于编译器的，后面找时间听完。

