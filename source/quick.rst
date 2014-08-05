.. _quick:

Quick start guide
*****************

Hardware requirements
---------------------

- Tower system for Kinetis K70F120M (with TWR-SER expansion)
- Mini USB type-B cable 
- Silica BrooklynBoard
- PC with at least one RS232 serial port and terminal software (two serial port for MAX3232 emulation)
- RS232 DB9 serial cable (modem type)
- Maxim Analog Essential Collection

.. image:: _static/SILICA_Brooklyn_Board.jpg

Software requirements
---------------------

- CodeWarrior MCU v10.3 Special Edition (`download here <http://www.freescale.com/webapp/sps/site/prod_summary.jsp?code=CW-MCU10&fpsp=1&tab=Design_Tools_Tab>`_).
- Brooklyn Board application firmware for TWR-K70F120M system (download here ....)

Hardware setup
--------------

- Assemble tower system TWR-K70F120M and Brooklin Board as in figure below.

.. image:: _static/assemble.jpg

| Don't care slot position, but be careful to connect Primary and Secondary connector properly. 
| Take care at reference signed near PCI board connectors.

.. image:: _static/pmod_pry.jpg

- Plug a Pmod Device (i.e. DS3231M Real Time Clock) inside properly connector.

.. image:: _static/pmod_in.jpg

**--> Be careful to see device reference next to connector. Each connector is designed for one or more devices and will only accept dedicated modules.**

- Plug Mini USB type-B cable into Cpu Board plug and connect to PC with Codewarrior. TWR power led will on. 

.. image:: _static/twr_on.jpg

- If you see device tab, you will find OSBDM/OSJTAG debug port. If it doesn't occour, **unplug USB cable, start Codewarrior and then plug USB cable**. Tower system will be found and OSBDM/OSJTAG driver will be loaded. Close Codewarrior suite.

.. image:: _static/twr_conn.jpg

- plug the standard serial DB9 cable into serial connector on Tower System

- connect serial cable to terminal PC (equipped with terminal SW)

.. image:: _static/serial.jpg

- On your terminal PC setup COMx parameter:

| speed = 115200 baud
| data with =  8
| parity = none
| stop bit = 1
| flow control = none

.. image:: _static/com_set.jpg 

Now you are ready for install FW project.


Brooklyn Board MQX FW setup
---------------------------

- In the root of your HDD C:\\ create new folder named "**Pmqx**". 

.. important:: **Pay attention that the pathname is case-sensitive**

.. image:: _new_image/Work_folder.jpg 

- Unzip all files from Pmod_MQX.zip into the folder **C:\\Pmqx** just created 

.. image:: _new_image/Work_project.jpg 

- **If you have already opened Codewarrior, exit and restart it**. The "Workspace launcher" tab will open. Clik on "brouse" button.  

.. image:: _static/set_wspace1.jpg

-  navigate and select **C:\\Pmqx** as workspace, then click OK

.. image:: _new_image/set_wspace.jpg

Now we could see the welcome window of Codewarrior Developement Suite

.. image:: _static/pmod3_welcome.jpg 

*maybe will open firewall popup as below*

.. image:: _static/pmod_fire.jpg 

if yes, left-clik on **enable access** and proceed

- close the welcome window by clicking '**X**' in the Welcome tab 

.. image:: _static/pmod_close_welcome.jpg 

Now we can see the Codewarrior main window

.. image:: _static/pmod_main.jpg 

Codewarrior is ready to setup MQX project

**IMPORTING AND BUILDING MQX LIBRARY**
--------------------------------------

- Navigate to  **C\\Pmqx\\config\\twrk70f120m\\cw10** and drag the file **twrk70f120m.wsd** into Codewarrior Project window

.. image:: _new_image/lib_imp.jpg 

BSP and PSP library (needed for this project) will be loaded automatically

.. image:: _static/set_lib.png 

Now you can see library in Project Window.

**BUILDING MQX LIBRARY**

- Click on hammer icon (with green star) red-circled as in figure below

.. image:: _new_image/lib_build.jpg 

- BSP and PSP library are now ready for the project

.. image:: _new_image/lib_build_1.jpg 

**IMPORTING Pmod1_6 FIRMWARE**
------------------------------

- Select File --> Import and click

.. image:: _static/pmod_import.jpg 

- in the next tab select "Existing Project into Workspace" and click "NEXT"

.. image:: _static/pmod_space.jpg 

- in the next window make the following step

| 1 - click on **Brouse** button.
| 2 - select folder "C:\\Pmqx\\Pmod1_6" as below.
| 3 - click on OK button.

.. image:: _new_image/p_imp_3.jpg 

- select checkbox "Pmod1_6(C:\\Pmqx\\Pmod1_6) 
- click "Finish"

.. image:: _new_image/p_imp_4.jpg 

The firmware Pmod1_6 will be imported

.. image:: _new_image/p_imp_5.jpg 


.. _How_to_build: 

**BUILDING Pmod1_6 FIRMWARE**
------------------------------

- see Codewarrior Project tab and select the project "Pmod1_6", move mouse cursor on the right side an arrow will appear. Click on arrow and a popup menu will open. Check "Pmod_MQX_FlashRam_debug" and click over

.. image:: _new_image/p_imp_6.jpg 

- select "Pmod1_6" project and right click over, select "Clean Project" and click

.. image:: _new_image/p_clean.jpg 

when process finish, click on single-hammer icon or righ-click over the project and select "build" to build entire project

.. image:: _new_image/build_prj.jpg

See the "problems" tab. There are 20 warnings because of file C_Events.c has same function as Events.c in BSP library. This is normally in MQX and doesn't make trouble

.. image:: _new_image/warn.jpg

Click on **bug** icon red-circled. Popup menu will open. Select "Pmod1_6_MQX_FLASH_RAM_debug" and click

.. image:: _new_image/debug.jpg

- Click again "bug" icon and debug will start with firmware download

during firmware download this tab will open 

.. image:: _new_image/down.jpg

and when download finish you see the main debug windows of Codewarrior

.. image:: _new_image/debug_ready.jpg

to start program you can press "F8" or click on Icon red-circled in image above

**NOTE: for full Codewarrior functionallity please refer to Freescale Official Guide**

`download here Codewarrior Guide <http://cache.freescale.com/files/soft_dev_tools/doc/support_info/Getting_Started_Guide_for_Microcontrollers.pdf?fsrch=1&WT_TYPE=Supporting%20Information&WT_VENDOR=FREESCALE&WT_FILE_FORMAT=pdf&WT_ASSET=Documentation&sr=11>`_

Running Brooklyn Board MQX FW
-----------------------------

When you start program, in terminal window you can see for few seconds this screen

.. image:: _new_image/mqx_start.jpg

this screen will inform about task init and task start

then, you see the Pmod start screen

.. image:: _new_image/first.jpg 

and after you can see the main menu

.. image:: _new_image/second.jpg 

| Now select device menu (typing selection key in the terminal window) and follow menu option to test device.
| **It' strongly recomended to change or insert Pmod Modules when Tower System is off (without power).** 
| Then, turn off the power by disconnecting the Mini USB B-type cable, remove device (if present) and insert new module in properly connector. 
| Turn on the power by plug the Mini USB B-type cable. The program will restart. No reload from debug console is needed. Follow same steps used before to test new device

