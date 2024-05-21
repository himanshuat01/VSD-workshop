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

     ## **DAY-2**
  To run floor plan, we have to give a command called as run_floorpan after you run simulation.   
  --> run_floorplan
  --> this will create a folder inside runs folder of designs's path of picorv32a.   
  planning will take a couple of minute to execute.
  After which the result would look like below given images.
![PDN-gen_succesful](https://github.com/himanshuat01/VSD-workshop/assets/114060372/df7d39c5-8cbc-4196-aca4-6c72408ec8f2)
--> To view the metals i.e., VMetal and HMetal (vertical metal and horizontal metal respt.) the details of so will be available in config.tcl of the newly generated file of floorplan after you run the command which is depicted below.
  ![FP-core-util](https://github.com/himanshuat01/VSD-workshop/assets/114060372/e8e9591a-6b8b-4b1f-a840-7667969df8cd)
  The folder which will be generated after running floor plan on that particular date would look something like this..
 ![runs_folder after floorplan](https://github.com/himanshuat01/VSD-workshop/assets/114060372/3e09085b-86ec-4d27-8b60-f1310aa11660)
--> To view the die area open def file present inside the floorplan folder.
  --> shown below 1micron is equal to 1000dbu (data base units).   
  ![image](https://github.com/himanshuat01/VSD-workshop/assets/114060372/3cd0b319-68e2-4086-8c1a-987c97bc2fc5)

  -->To view floorplan in MAGIC (opensource softare for layouts) we have to invoke it by calling **magic -T** along with the path of rcfile wwhich describres about the technology we are using. Here the **-T** switch is used to define the technology node.   
  --> home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
  *The tool will look as below, here we have opened picorv32a' layout.
  ![layout_opened_in_magic](https://github.com/himanshuat01/VSD-workshop/assets/114060372/fec5e8ac-327d-46f5-8171-4d26ae0c0bf9)
  I would like to mention on few points here:      
  1). The path and invoking command for Magic.   
  2). DRC - Design rule check. Certain rules set by the Fab unit for every particular pdk to follow for proper fabrication.       
  3). The technology node which is sky130A.    
  4). All different layers avaliable to use.     
--> Along with the layout window there is another window called the tkcon window used to type commands and for automating.    
  ![tkcon_window](https://github.com/himanshuat01/VSD-workshop/assets/114060372/3a48609a-f014-4732-88c3-ab8bc8e7d4cc)
  * Above arrowed image depicts the **tkcon** window.
    --> The next step is to run placement by using te command **run_placement**.
    This will take a while to execute as there are many iterations to be performed.
    --> Once it is completed the terminal will have it like this.
    ![runplacementcompl](https://github.com/himanshuat01/VSD-workshop/assets/114060372/5ba35b90-4b46-4600-877e-0d76bddcf05c)
  --> To view placement in MAGIC we have to open magic along with reading the picorv32a placement.def file with the help of below command.
  -->magic -T /home/vsdworkshop/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
* Once tool is invoked along with pre placed blocks all other blocks are placed too.
  ![placement_opened_in_magic](https://github.com/himanshuat01/VSD-workshop/assets/114060372/c85eedbf-df56-429a-8409-71dd6b01d8f1)
  ![interior_view_of_placement](https://github.com/himanshuat01/VSD-workshop/assets/114060372/85248feb-1adc-445a-8df1-b286daffa601)
  * To view Decoupling capacitors we need to zoom-in to boundries of the cell which is shown below here,
  ![decaps in placement](https://github.com/himanshuat01/VSD-workshop/assets/114060372/15fc1ff5-73d4-4e50-83fa-cb63fd701536)



    ## **DAY-3**

      --> To view the layout of standard cell inverter in magic tool we invoke it by copying the tech file and call it with the mag file. Once its done magic tool opens and the inverter's layout will look something like this.
    ![inv_in_magic](https://github.com/himanshuat01/VSD-workshop/assets/114060372/f9345667-7f8e-498f-8570-ff1be26fd0c4)
    * now lets extract it spice format by **giving ext2spice** in tkcon window.     
    * The spice file will be generated and will be stored in pwd.
      ![spice_extracted](https://github.com/himanshuat01/VSD-workshop/assets/114060372/a3cb2db1-050c-4a18-8593-cacf82a775aa)
      
      --> To view the spice generated file we have to give the command **vim sky130_inv.spice**.   
      ![contents_inside_spice_file](https://github.com/himanshuat01/VSD-workshop/assets/114060372/a9096075-d7cd-4a6e-ad10-1ca3ad26bae4)

        --> we have to edit few lines of code after which it is
      ![code_edited](https://github.com/himanshuat01/VSD-workshop/assets/114060372/c37bfe82-5172-4944-83cd-be2073d161e2)

      after running the command **ngspice sky130_inv.spice** we get the total outputs and to plot it we give another command based on the nodes available.
      --> plot y vs time a we get the output of transient analysis.
      ![transient_analysis_inv](https://github.com/himanshuat01/VSD-workshop/assets/114060372/ed440302-6c78-4b8f-80a6-30c8e4d698ff)
      
Rise time = 0.10ns
Fall time = 0.09ns   

    ![fall_time](https://github.com/himanshuat01/VSD-workshop/assets/114060372/71584bca-2c20-48d2-9ad7-963ce9b0cb0c)  
    
  After downloading the required files from git by using wgit, then by running the command magic -d XR we can openout magic tool
  and start working. Here we open an already exisiting file i.e., met3 which looks like this.
  ![met3](https://github.com/himanshuat01/VSD-workshop/assets/114060372/ec4e6a72-27cf-43b4-898f-35ce1b5fa74a)
  view after loading poly:
   ![load_poly](https://github.com/himanshuat01/VSD-workshop/assets/114060372/c0a3c9c9-536d-4ccf-bc0e-07bd04bbeee2)   
   
After adding n-diff and p-diff, we get:  
 ![addn_ndiff_pdiff](https://github.com/himanshuat01/VSD-workshop/assets/114060372/8bc3da47-15da-4a1c-80e3-9af33dd2dc39)   

   To find the tracks present we can go to the track info file present inside pdks of openlane.   
   ![tracks present inside openlane](https://github.com/himanshuat01/VSD-workshop/assets/114060372/97cfe349-9da6-4309-812c-cf18651bb756)   


  ## **DAY-4**   

    
  --> Setting up of grid   
![grid_setup](https://github.com/himanshuat01/VSD-workshop/assets/114060372/58c993d9-8be2-4d03-a41f-a9af30fcfd25)   
--> to get a lef file we use a command call **lef write** in tkcon window.   
![to_create_lef_file](https://github.com/himanshuat01/VSD-workshop/assets/114060372/c00cc428-e6c3-40c7-b6d9-1e7a0c55fab2)   
--> to view contents inside this file go back to main terminal and check for any .lef files present inside pwd.
lef file would look like this.   
![inside_lef_file-window](https://github.com/himanshuat01/VSD-workshop/assets/114060372/2b9406e7-8af4-4756-b4b4-323f36254499)    





   
      

   
    



    

    

    
      





    



    









  

 

  
  
  


  




  

  
  




  




















