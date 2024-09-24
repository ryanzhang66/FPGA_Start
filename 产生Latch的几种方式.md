# 产生Latch的几种方式

## 正确的代码

这里我们实现了对于译码器的FPGA源码
- 使用if-else语句进行译码
    ```v
    module decoder(
        input wire in_1,
        input wire in_2,

        output reg out
    );

    always@(*) begin
        if ({in_1, in_2} == 2'b00)
            out = 1'b0;
        else if ({in_1, in_2} == 2'b01)
            out = 1'b1;
        else if ({in_1, in_2} == 2'b10)
            out = 1'b0;
        else if ({in_1, in_2} == 2'b11)
            out = 1'b1;
        else 
            out = 1'b0;
    end
    endmodule
    ```
    - 编译后生成的电路图为：
        
- 使用case语句进行译码
    ```v
    module decoder(
        input wire in_1,
        input wire in_2,

        output reg out
    );

    always@(*) begin
        case ({in_1, in_2})
            2'b00: out = 1'b0;
            2'b01: out = 1'b1;
            2'b10: out = 1'b0;
            2'b11: out = 1'b1;
            default: out = 1'b0;
    end
    endmodule
    ```

## 1. 组合逻辑中赋值给自己

我这里直接用源码演示