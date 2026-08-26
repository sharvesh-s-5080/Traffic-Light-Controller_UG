# Traffic-Light-Controller_UG
## Experiment: Write and Simulate Traffic Light Controller using Verilog HDL and Verify with Testbench

## Aim

To design and simulate a Traffic Light Controller using Verilog HDL and verify its functionality using a testbench in Xilinx Vivado.

## Apparatus Required

* Computer System
* Xilinx Vivado Design Suite
* Verilog HDL Simulator (Vivado Simulator)
* Windows/Linux Operating System

## Procedure

1. Open Xilinx Vivado and create a new RTL project.
2. Create a Verilog source file named **traffic_light.v**.
3. Write the Verilog HDL code for the Traffic Light Controller.
4. Create a testbench file named **traffic_light_tb.v**.
5. Apply clock and reset signals through the testbench.
6. Run Behavioral Simulation.
7. Observe the output waveforms for Red, Yellow, and Green signals.
8. Verify the correct sequence of traffic light transitions.
9. Record the simulation results.

## Verilog HDL Code

```verilog
module traffic_light(
    input clk,
    input reset,
    output reg Red,
    output reg Yellow,
    output reg Green
);

reg [1:0] state;

parameter RED_STATE    = 2'b00,
          GREEN_STATE  = 2'b01,
          YELLOW_STATE = 2'b10;

always @(posedge clk or posedge reset)
begin
    if(reset)
        state <= RED_STATE;
    else
    begin
        case(state)
            RED_STATE:    state <= GREEN_STATE;
            GREEN_STATE:  state <= YELLOW_STATE;
            YELLOW_STATE: state <= RED_STATE;
            default:      state <= RED_STATE;
        endcase
    end
end

always @(*)
begin
    case(state)
        RED_STATE:
        begin
            Red = 1;
            Yellow = 0;
            Green = 0;
        end

        GREEN_STATE:
        begin
            Red = 0;
            Yellow = 0;
            Green = 1;
        end

        YELLOW_STATE:
        begin
            Red = 0;
            Yellow = 1;
            Green = 0;
        end

        default:
        begin
            Red = 1;
            Yellow = 0;
            Green = 0;
        end
    endcase
end

endmodule
```

## Testbench Code

```verilog
`timescale 1ns/1ps

module traffic_light_tb;

reg clk;
reg reset;

wire Red;
wire Yellow;
wire Green;

traffic_light uut(
    .clk(clk),
    .reset(reset),
    .Red(Red),
    .Yellow(Yellow),
    .Green(Green)
);

always #5 clk = ~clk;

initial
begin
    clk = 0;
    reset = 1;

    #10 reset = 0;

    #60;

    $finish;
end

endmodule
```

## Expected Output
<img width="1432" height="237" alt="image" src="https://github.com/user-attachments/assets/4fd6b86c-82a5-4d76-9016-bd0701150735" />


## Result

The Traffic Light Controller was successfully designed and simulated using Verilog HDL. The output waveform verified the correct sequence of Red → Green → Yellow → Red.

## Conclusion

Thus, the Traffic Light Controller was implemented and verified successfully using Verilog HDL in Xilinx Vivado. The simulation results confirmed the correct operation of the finite state machine and the expected traffic light sequence.
