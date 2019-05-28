---
layout: post
tags: verilog
---

# vlog_eday
by WeiLin, 2019.5.23

**Verilog Everyday(Updating.....)**

vlog_eday是一个技术群里提出的想法，就是每天由群主布置作业，成员按时完成作业并提交，如果连续三天未提交作业，就会被退群。虽然这个“课堂”只维持了2个星期，但也是学到了很多东西，这里很感谢[“不忘出芯”](https://github.com/ic7x24)及[“陈锋”](http://exasic.com/)。

vlog_eday大部分例子是按照下面参考书来进行的。vlog_eday并没有对详细原理进行介绍，大多是自己的总结，更侧重于代码，所以关于详细的理论请参考参考书。我将自己写的code和testbench放在了[这里](https://github.com/xLinWei/vlog_eday)。代码中大部分都经过 _Modelsim_ 仿真测试过，如果有任何错误，请指正。

### Reference book
[1] William J.Dally,R.Curtis Harting.数字设计系统方法[M].  
[2] Kishore Mishra.Verilog高级数字系统设计技术与实例分析[M].

### Content

[day1:进制与编码](./vlog_day01.html)
：进制简介/BCD编码

[day2:组合逻辑](./vlog_day02.html)
：基本逻辑/组合逻辑

[day3:边沿检测](./vlog_day03.html)
：同步边沿检测/异步边沿检测

[day4:加法器](./vlog_day04.html)
：半加器/全加器/行波进位加法器/溢出检测

[day5:计数器](./vlog_day05.html)
：二进制计数器/环形计数器/约翰逊计数器/格雷码计数器

[day6:按键去抖动](./vlog_day06.html)
：按键去抖动

[day7:格雷码](./vlog_day07.html)
：Bin2Gray/Gray2bin

[day8:LFSR](./vlog_day08.html)
：斐波那契LFSR/伽罗瓦LFSR/LFSR计数器

[day9:校验码](./vlog_day09.html)
：奇偶校验/CRC校验

[day10:译码和编码](./vlog_day10.html)
：7段译码器/常规编码器/优先编码器

[day11:时钟分频](./vlog_day11.html)
：偶数分频/奇数分频

[day12:复位](./vlog_day12.html)
：同步复位/异步复位/异步复位同步释放

[day13:锁存器](./vlog_day13.html)
：避免锁存器的代码书写规范

[day14:BCD加法器](./vlog_day14.html)
：BCD加法器/`a[base-:width]`结构的使用

[day15:Mux选择器](./vlog_day15.html)
：向量索引in[sel]实现选择器/bit切片确定固定宽度

[day16:有限状态机](./vlog_day16.html)
：状态机分类/状态机的3种写法

[day17:亚稳态](./vlog_day17.html)
：亚稳态是什么/为什么需要建立保持时间

[day18:同步FIFO](./vlog_day18.html)
：同步FIFO的代码

[day19:同步技术](./vlog_day19.html)
：两级触发器/脉冲同步器

[day20:异步FIFO](./vlog_day20.html)
：异步FIFO代码