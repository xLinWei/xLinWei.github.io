---
layout: post
tags: verilog
---

## vlog_day2:逻辑电路 
by [WeiLin](https://github.com/xLinWei)

### 一、基本逻辑
Verilog里有操作符可以实现基本逻辑运算，总结如下：
```
逻辑操作符：&&  ||  !
按位操作符：&  |  ~  ^  ~^
归约操作符：&  ~&  |  ~|  ^  ~^
```
注意：逻辑操作里只有“与或非”，没有异或；归约操作里没有“非”，因为“非”是一元操作。

### 二、组合逻辑
任意组合逻辑均可以表示成“与或非”的组合，这是因为最小表达式中就只有“与或非”。与非门和或非门又称作通用逻辑门，所有门均可以用**与非门、或非门**表示，在实际中一般使用与非门:
```
~ x = nand(x, x)
x & y = ~(nand(x, y))
x | y = ~( ~x & ~y )    //德摩根定理
```
_为什么是与非门，而不是与门？_ 这是因为静态CMOS门电路只能构造反相逻辑，像与非、或非，其它非反相逻辑需要多级CMOS门。_那么为什么是与非门，而不是或非门？_ **这是因为在相同面积下与非门的速度更快。**
(_有一门课叫[Nand2Tetris](https://www.coursera.org/learn/build-a-computer)，这门课就是用与非门搭建一个计算机，感兴趣的可以听下。_)


### _**Exercise:**如何用MUX实现全加器？_

全加器可以表示如下：
```
sum = a^b^cin;
cout = (a & b) | (a & cin) | (b & cin);
```
所以首先需要用MUX实现“与、或、非”操作：
```
设MUX(in0,in1,sel,out),则：
out=x&y <=> MUX(0,y,x,out)
out=x|y <=> MUX(y,1,x,out)
out=!x <=> MUX(1,0,x,out)
```
而异或`z=xy'+x'y`可以表示如下,然后据此就可以构建全加器了。

<center><img src="image/02_xor.png" width="40%"></center>

从上面的Exercise可以看出，MUX能够实现“与门、或门、非门、异或”等逻辑门。一般在 _ECO(Engineering Change Order,工程设计变更)_ 阶段需要使用替补元件或额外的元件对电路进行修正，这时使用MUX就很方便。