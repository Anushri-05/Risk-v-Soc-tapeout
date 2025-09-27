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

## SCREENSHOT OF EXECUTION 



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

  
