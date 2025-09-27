# week1 covers introduction to verilog RTL design and synthesis using yoysy, iverilog and gtkwave
## running a RTL code testbench and observe the waveform as output 
```bash 
module good_mux (input i0 , input i1 , input sel , output reg y); // 2:1 mux 
always @ (*)
begin
        if(sel)
                y <= i1;
        else
                y <= i0;
end
endmodule
```

TESTBENCH 
```bash
`timescale 1ns / 1ps
module tb_good_mux;
        // Inputs
        reg i0,i1,sel;
        // Outputs
        wire y;

        // Instantiate the Unit Under Test (UUT)
        good_mux uut (
                .sel(sel),
                .i0(i0),
                .i1(i1),
                .y(y)
        );

        initial begin
        $dumpfile("tb_good_mux.vcd");
        $dumpvars(0,tb_good_mux);
        // Initialize Inputs
        sel = 0;
        i0 = 0;
        i1 = 0;
        #300 $finish;
        end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
```
## commands to get waveform
 
$ iverilog good_mux.v tb_good_mux.v
$ ./a.out
$ gtkwave tb_good_mux.vcd

## SCREENSHOT OF EXECUTION 

<img width="1181" height="690" alt="Screenshot from 2025-09-27 21-22-39" src="https://github.com/user-attachments/assets/2e90334f-8784-4c30-87e4-74c45909340e" />


## LOGIC SYNTHESYS USING TOOL YOSYS 
INTRODUCTION :
What is synthesys -- the process of converting RTL code to gate level netlist. 
* the design is converted into gates and the connections are made between the gates, this is given out as a file called Netlist.
Inputs and Outputs of synthesys




To Verify the synthesys : give the netlist which is output of synthesys and the testbench to the iverylog and oberver the waveform in gtkwake 

## commands to run synthesys in yosys 
``` bash 
yosys // invoke the yosys tool in the terminal
read_liberty -lib /lib/sky130_hd.lib
read_verilog good_mux.v 
synth -top good_mux
abc -liberty 
show
write_verilog mux_netlist.v 
write_verilog -noattr mux_netlist.v //alternate command to see the netlist file
```
## screenshot 
  <img width="1214" height="768" alt="Screenshot from 2025-09-27 17-26-02" src="https://github.com/user-attachments/assets/f76f91a0-d2dd-4770-aae8-67f307930a24" />
  <img width="525" height="201" alt="Screenshot from 2025-09-27 17-27-35" src="https://github.com/user-attachments/assets/76af45b5-493a-4e03-93cf-5d2537ed8246" />



