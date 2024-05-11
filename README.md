**INTRODUCTION**
Hello all!
As a part of 5-day workshop on VLSI-SOC and design, I'm uploading the contents thought and learnt.

--> Learnt importance of VLSI and Semiconductor Industry.
--> Took an example of ARDUINO microcontroller Board to understand the importance of main 'chip' present on it.
--> There are different types of packaging a chip such as QFN(quad flat no-leads), DIP(dual-in line pacakging), TO packaging and other different types.
'PADS' are also an important component present inside of a chip. It is basically used for flow of signals inside and outside of the chip.
The word 'FOUNDRY' is critical. Performance of all chips are dependant on Founfries.
VLSI engineers communicate with foundries.

'MACROS' are pure digital blocks inside a chip.
Here I'll be speaking few words on ASIC flow of RTL to GDSII
![Screenshot (487)](https://github.com/himanshuat01/VSD-workshop/assets/114060372/3501fbcc-f9bc-41ae-8d26-25e2c0378168)

Here the first step is getting an RTL
--> RTL stands for Register-Transfer-Level. We can write a Verilog code or a VHDL code for an RTL.
--> Synthesis is nothing but converting RTL code to its equal component level blocks from the standard cell library (SCL).
--> FP+PP stands for floor planning and Placement planning where the first term defines where the particular component has to be, what size and shape should it be. The latter involves binding of netlist with physical cells.
--> CTS stands for clock tree synthesis which is a process used for distributing clock signal equally among all comoponents.
--> Routing is making physical connectionns(links) between signal pins using metal layer.
--> And then Sign-off is nothing but to verify the design before going for tapeout.
--> GDS- Graphic design system is the final output product or file which is to be given to foundry for the IC to get it manifactured.



