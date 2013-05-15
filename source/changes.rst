Firmware changes
****************

1 - added include file **MaxFuncRedefinition.h** at the top of **MaximPmod.c** file. 
    This file must be the first to be included in the list.

::

 #include "MaxFuncRedifinition.h"  <----

 #include <stdio.h>
 #include "platform.h"
 #include "menu.h"
 #include "utilities.h"
 #include "maximDeviceSpecificUtilities.h"
 #include "maximPMOD.h"

 #define MAJOR_REVISION 1
 #define MINOR_REVISION 6


2 - renamed **main()** function inside **MaximPmod.c** file with new name **main_pmod()**.

::

 int main_pmod()      <----
 /**
 * \brief       Main() function for Analog Essentials example program.
 * \par         Details
 *              This function allows you to set and initializes the FPGA and hardware, which will appear in the main menu by
                HyperTerminal, which will send the demo of individual programs to the basic module.
 *
 * \param       None
 *
 * \retval      Always TRUE
 */
 {
	// Variables for the main() function
	u8 uchInput=0;
	int nMenuState=0;
	int i=0;
	char tempString[256];
 
3 - commented function **led_knight_rider** inside **MaximPmod.c** file to obtain application fast start.

::

 // Toggle the LEDs so that the user knows the board is awake
	XGpio_Initialize(&g_xGpioLed, XPAR_AXI_GPIO_LED_DEVICE_ID);
	XGpio_SetDataDirection(&g_xGpioLed, 1, 0x00000000); // Set the LED peripheral to outputs
 // 	led_knight_rider(&g_xGpioLed,2);     <----
 
4 - changed costant definition **ABOUT_ONE_SECOND** inside **MaximPmod.h** file as follow:

::

 #define ABOUT_ONE_SECOND 74067512/8/3   <----
 //#define ABOUT_ONE_SECOND 74067512      //!< approx 1 second delay when used as argument with function delay(numberCyclesToDelay)
 // Update this if uBlaze/Zynq CPU core frequency is changed, or if the external memory timing changes.
 // Although emprirically tested to 1.0000003 seconds, it is not meant to be used for precise timing purposes
	
**NOTE: All these changes are tested on revision 1.6 of Maxim project files and need to be checked on further new revisions**

