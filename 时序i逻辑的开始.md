# 时序逻辑的开始

## D触发器
寄存器的开始，每个D触发器能够存储一位二进制码。  
- D触发器有三个输入信号：
  - `sys_clk`：时钟信号
  - `D`：数据输入信号
  - `sys_rst_n`：复位信号，低电平有效
  - `Q`：输出信号

## 同步复位
这个好理解，因为我们引入了时钟信号，作用就是同步信号。  
但在需要复位时，时钟信号出现了问题，就无法正常复位，所以同步复位的电路稳定性较差。    

## 异步复位，同步释放
既然复位受是信号的影响而导致电路稳定性较差，那么我们就让**复位不受时钟信号的影响**。  
但是这样我们会导致**复位后的信号位置不确定**，这对时序逻辑电路的设计有很大的影响。  
所以我们需要同步释放复位信号，让**复位的信号与时钟上升沿对齐**。  

## D触发器的FPGA实现
- 源代码
  ```v
  module d_trigger(
      input wire sys_clk,
      input wire D,
      input wire sys_rst_n,

      output reg Q
  );

  always@(posedge sys_clk) begin
      if (sys_rst_n == 1'b0) begin 
          Q <= 1'b0;
      end 
      else begin
          Q <= D;
      end
  end
  endmodule
  ```
  - 进行编译后，生成的电路图是这样的：
      ![alt text](image.png)
