# **INTRODUCTION**  
Hello all!  
As a part of 5-day workshop on VLSI-SOC and design, I'm uploading the contents thought and learnt.  
  
--> Learnt importance of VLSI and Semiconductor Industry.  
--> Took an example of ARDUINO microcontroller Board to understand the importance of main 'chip' present on it.  
--> There are different types of packaging a chip such as QFN(quad flat no-leads), DIP(dual-in line packaging), TO packaging and other different types.  
'PADS' are also an important component present inside of a chip. It is basically used for flow of signals inside and outside of the chip.  
The word 'FOUNDRY' is critical. Performance of all chips are dependant on Founfries.  
VLSI engineers communicate with foundries.  
    
'MACROS' are pure digital blocks inside a chip.  
Here I'll be speaking few words on ASIC flow of RTL to GDSII  
![Screenshot (487)](https://github.com/himanshuat01/VSD-workshop/assets/114060372/3501fbcc-f9bc-41ae-8d26-25e2c0378168)
  
Here the first step is getting an RTL  
--> RTL stands for Register-Transfer-Level. We can write a Verilog code or a VHDL code for an RTL.  
--> Synthesis is nothing but converting RTL code to its equal component level blocks from the standard cell library (SCL).   
--> FP+PP stands for floor planning and Power planning where the first term defines where the particular component has to be, what size and shape should it be. The latter involves binding of netlist with physical cells.  
--> CTS stands for clock tree synthesis which is a process used for distributing clock signal equally among all comoponents.  
--> Routing is making physical connectionns(links) between signal pins using metal layer.  
--> And then Sign-off is nothing but to verify the design before going for tapeout.  
--> GDS- Graphic design system is the final output product or file which is to be given to foundry for the IC to get it manifactured.  



# **INVOKING THE TOOL**  
### **DAY-1**  

since we are using linux os (ubuntu 64 bit) there is a bit of bash programming to be done in order to invoke the tool **OPENLANE**  
--> The tool is present in the work folder of desktop.  
--> work  
--> tools  
--> openlane_working_dir  
--> openlane  
and then inside the tool are many files related, here we will be looking into few files such as designs, config.tcl and so on  
to invoke the tool  
--> type 'docker'  
and then for startin the tool we give the command ./flow.tcl -interactive  
So now you will be able to see the openlane tool invoked in the terminal itself.  
Now you should be able to see a screen something like this  
![openlane_start](https://github.com/himanshuat01/VSD-workshop/assets/114060372/20713412-5fd2-4418-b744-76ec03921139)  
And to see different projects present inside the design folder, you can separately do that as well.  
Here i have opened the designs folder to show the number of projects.  
![openlane_start](https://github.com/himanshuat01/VSD-workshop/assets/114060372/c4a1fcfc-b0e9-4e50-8139-d36af24f846d)  

  # **Running Simulations**   
  
Now we will be working on synthesis of picorv32a.  
Before synthesis we need to prepare run folder inside the project folder of designs.  
--> can be done by runnning the command 'prep-design picorv32a'  
![prep_complete](https://github.com/himanshuat01/VSD-workshop/assets/114060372/fee4533d-98b4-47fb-9b70-a87769b8c58c)  
--> To check wether the runs folder is created or no we can take a look at the contents inside picorv32a.  
Below image marked for the presence of folder with the date of  creation.  
![run_folder_inside_picorv32a](https://github.com/himanshuat01/VSD-workshop/assets/114060372/0a03e0d1-4346-4722-8fd1-fa07ceba59c3)  

  **Now that Preparation is done we can move on to synthesis.**   
--> Run command run_synthesis. It will take few minutes to execute and if any errors are present it would pop up here.  
after completion you will receive a return which would look something like this.  
![image](https://github.com/himanshuat01/VSD-workshop/assets/114060372/16223132-498f-4544-a748-40a7b9b9b2cc)  
* above image shows synthesis successful.
* Our one of the objective from this is to find the flop ratio which is the ratio of total number of Dff's to the total number of cells in the design.  
* It can be noticed in the below image that the total number of Dff's are 1634 and the total number of cells are 17323.
* The ratio comes out to be 0.09432 and in percentage comes to be 9.432.
  ![image](https://github.com/himanshuat01/VSD-workshop/assets/114060372/bb266198-48d5-437b-b88d-d448b44e4c93)
  




  




















