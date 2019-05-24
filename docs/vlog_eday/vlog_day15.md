---
layout: post
tags: verilog
---

## vlog_day15:Mux选择器
by [WeiLin](https://github.com/xLinWei)

选择器用case和if...else...语句即可。但有时也可以用in[sel]来直接选择，如下8选1：
```verilog
module Mux8to1( 
    input [7:0] in,
    input [3:0] sel,
    output out );

    assign out=in[sel];

endmodule
```
用向量索引(in[sel])来做选择器相比于case语句更简洁，但是这种写法有限制:“Vector indices can be variable, as long as the synthesizer can figure out that the width of the bits being selected is constant. ”

如下例，从in[7:0]中根据sel选择2bit，如果使用`assign out=in[sel*2+1:sel*2];`就会报错‘Range must be bounded by constant expressions.’
```verilog
module mux(
    input [7:0] in,
    input [1:0] sel,
    output [1:0] out
);

assign out=in[sel*2+1:sel*2];
//error:Range must be bounded by constant expressions.

endmodule
```
这时候就可以使用bit slicing(bit切片)，也就是day14里的a[base-:width]结构，这样综合器就可以确定bit宽度为constant.
```verilog
module mux(
    input [7:0] in,
    input [1:0] sel,
    output [1:0] out
);

assign out=in[sel*2+1-:2];

endmodule
```