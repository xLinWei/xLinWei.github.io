---
layout: post
tags: verilog
---

## vlog_day19:同步技术
by [WeiLin](https://github.com/xLinWei)

### 1.两级触发器
两级触发器适合从慢时钟域到快时钟域，而且需要注意两级触发器只能同步单bit数据：
```verilog
//同步技术1：两级触发器
module sync1(
    input clk,rst_n,
    input din,
    output reg dout
);

reg din_r;
always@(posedge clk or negedge rst_n)begin
    if(!rst_n)
        dout<=0;
        din_r<=0;
    else begin
        din_r<=din;
        dout<=din_r;
    end
end

endmodule
```

### 2.脉冲同步器
如果是从快时钟域到慢时钟域就需要使用脉冲同步器，其思想是将脉冲展宽以便采集：
```verilog
//同步技术2：脉冲同步器
module sync2(
    input clka,
    input clkb,
    input rst_n,
    input pluse_src,
    output pluse_dest
);

reg sig_stretched;//pluse_src展宽后的信号
wire sig_stretched_ack_edge;//ack信号的边沿信号，用于将sig_stretched拉低
always@(posedge clka or negedge rst_n)begin
    if(!rst_n)
        sig_stretched<=0;
     else begin
        if(sig_stretched_ack_edge)
            sig_stretched<=0;
        else if(pluse_src)
            sig_stretched<=1;
        else
            sig_stretched<=sig_stretched;
     end
end

reg sig_stretched_sync;//两级同步器的中间信号
reg sig_stretched_dest;//sig_stretched同步到clkb后的信号
reg sig_stretched_dest_d1;//sig_stretched_dest延时信号，用于上升沿检测
always@(posedge clkb or negedge rst_n)begin
    if(!rst_n)begin
        sig_stretched_sync<=0;
        sig_stretched_dest<=0;
        sig_stretched_dest_d1<=0;
    end
    else begin
        sig_stretched_sync<=sig_stretched;
        sig_stretched_dest<=sig_stretched_sync;
        sig_stretched_dest_d1<=sig_stretched_dest;
    end
end
//上升沿检测，输出脉冲
assign pluse_dest=sig_stretched_dest & !sig_stretched_dest_d1;

reg sig_stretched_sync1;//两级触发器中间信号
reg sig_stretched_ack;//sig_stretched_dest同步到clka后的信号
reg sig_stretched_ack_d1;//sig_stretched_ack延时信号,用于上升沿检测
always@(posedge clka or negedge rst_n)begin
    if(!rst_n)begin
        sig_stretched_sync1<=0;
        sig_stretched_ack<=0;
        sig_stretched_ack_d1<=0;
    end
    else begin
        sig_stretched_sync1<=sig_stretched_dest;
        sig_stretched_ack<=sig_stretched_sync1;
        sig_stretched_ack_d1<=sig_stretched_ack;
    end
end
//ack信号的边沿信号，用于将sig_stretched拉低
assign sig_stretched_ack_edge=sig_stretched_ack & !sig_stretched_ack_d1;

endmodule
```

当然还有很多其他的同步技术，比如握手机制、异步FIFO，后面会介绍异步FIFO。

