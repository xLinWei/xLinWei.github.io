---
layout: post
tags: verilog
---

## vlog_day20:异步FIFO
by [WeiLin](https://github.com/xLinWei)

推荐2个讲解异步FIFO不错的博客：  
https://zhuanlan.zhihu.com/p/42991844  
https://ninghechuan.com/2018/12/15/Verilog%E8%AE%BE%E8%AE%A1%E5%BC%82%E6%AD%A5FIFO/  

**1.关于写满读空怎么判断**：当什么都不写时rd_ptr==wr_ptr，当写满时rd_ptr也等于wr_ptr，所以有两个解决办法：  
- 将地址扩展1位，表示读写指针是否在同一轮，所以在判断空满时如果rd_ptr==wr_ptr则为空，如果最高位不等其余位相等则为满(这里是用二进制表示指针计数)。而在格雷码下判断满状态时除了最高位不等次高位也要不等。  
- FIFO少写一个，rd_ptr==wr_ptr为空，rd_ptr==wr_ptr+1（rd_ptr，wr_ptr指向即将要处理的位置）。

**2.关于格雷码同步**：将写时钟域的写指针同步到读时钟域，将同步后的写指针与读时钟域的读指针进行比较产生读空信号；将读时钟域的读指针同步到写时钟域，将同步后的读指针与写时钟域的写指针进行比较产生写满信号；而同步后的读指针或写指针会延时两个时钟，所以会造成假满和假空的状态，这会导致满空趋于保守，但是保守并不等于错误。

**3.二进制码转换成二进制格雷码**：其法则是保留二进制码的最高位作为格雷码的最高位，而次高位格雷码为二进制码的高位与次高位相异或，而格雷码其余各位与次高位的求法相类似。这样就可以实现二进制到格雷码的转换了，总结就是移位并且异或，verilog代码实现就一句：
assign graydata = (bindata >> 1) ^ bindata;

4.FIFO深度：通过读写频率，突发速率，突发长度进而确定FIFO的最小深度。要理解“背靠背“突发。https://ninghechuan.com/2019/01/20/%E4%BD%A0%E9%97%AE%E6%88%91FIFO%E6%9C%89%E5%A4%9A%E6%B7%B1/

```verilog
//异步FIFO
module asunc_fifo#(
    parameter FIFO_DEATH=16,
    parameter FIFO_WIDTH=8
)(
    input clk1,//写时钟
    input rst1,
    input we,//写使能
    input [FIFO_WIDTH-1:0]din,

    input clk2,//读时钟
    input rst2,
    input re,//读使能
    output reg [FIFO_WIDTH-1:0]dout,

    output full,
    output empty
);

localparam ADDR_WIDTH=$clog2(FIFO_DEATH);

reg [FIFO_WIDTH-1:0] RAM [FIFO_DEATH-1:0];

reg [ADDR_WIDTH:0] w_ptr;//需要多1位
always@(posedge clk1 or posedge rst1)begin
    if(rst1)
        w_ptr<=0;
    else begin
        if(we && !full)begin
            RAM[w_ptr]<=din;
            w_ptr<=w_ptr+1;
        end
        else
            w_ptr<=w_ptr;
    end
end

reg [ADDR_WIDTH:0] r_ptr;//需要多1位
always@(posedge clk2 or posedge rst2)begin
    if(rst2)
        r_ptr<=0;
    else begin
        if(re && !empty)begin
            dout<=RAM[r_ptr];
            r_ptr<=r_ptr+1;
        end
        else
            r_ptr<=r_ptr;
    end
end
////////指针同步/////////
reg [ADDR_WIDTH:0] w_ptr_g;//gray写指针
bin2gray #(ADDR_WIDTH+1) bg1(w_ptr,w_ptr_g);

reg [ADDR_WIDTH:0] w_ptr_g1;//两级同步器中间值
reg [ADDR_WIDTH:0] w_ptr_s;//同步后的写指针
always@(posedge clk1 or posedge rst1)begin
    if(rst1)begin
        w_ptr_g1<=0;
        w_ptr_s<=0;
    end 
    else begin
        w_ptr_g1<=w_ptr_g;
        w_ptr_s<=w_ptr_g1;
    end
end


reg [ADDR_WIDTH:0] r_ptr_g;//gray读指针
bin2gray #(ADDR_WIDTH+1) bg2(r_ptr,r_ptr_g);

reg [ADDR_WIDTH:0] r_ptr_g1;//两级同步器中间值
reg [ADDR_WIDTH:0] r_ptr_s;//同步后的读指针
always@(posedge clk2 or posedge rst2)begin
    if(rst1)begin
        r_ptr_g1<=0;
        r_ptr_s<=0;
    end 
    else begin
        r_ptr_g1<=r_ptr_g;
        r_ptr_s<=r_ptr_g1;
    end
end
////////空满判断////////
assign full=((!w_ptr_g[ADDR_WIDTH-:2]==r_ptr_s[ADDR_WIDTH-:2])&&(w_ptr_g[ADDR_WIDTH-2:0]==r_ptr_s[ADDR_WIDTH-2:0]))?1:0;
assign empty=(r_ptr_g==w_ptr_s)?1:0;

endmodule
```