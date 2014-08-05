Firmware changes
****************

**1** - added include file **MaxFuncRedefinition.h** at the top of **MaximPmod.c** file. This file must be the first include in list.

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
 
**2** - renamed **main()** function inside **MaximPmod.c** file with new name **main_pmod()**.

::

 int main_pmod()      <----
 /**
 * \brief       Main() function for Analog Essentials example program.
 * \par         Details
 *              This function sets up and initializes the FPGA and hardware, displays the root menu via
 *              Hyperterminal, then dispatches inidividual demo programs for specific module based on
 *              user's keypress selection.
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
	
**3** - Added redefinition of "printf" function inside include file **maximPMOD.h**. This is needed for build this project without any other changes to send functionality messages through Tower Expansion Board serial interface

::

 #ifndef MAXIMPMOD_H_
 #define MAXIMPMOD_H_

 #include "xgpio.h"
 #include "xgpio_l.h"
 #include "xparameters.h"
 #include "xuartlite.h"
 #include "xspi_l.h"
 #include "xspi.h"
 #include "xiic_l.h"
 #include "utilities.h"
 #include <string.h>
 #include <stdio.h>
 #include "platform.h"
 #include "math.h"

 **#define printf _io_printf         <----**

 #define DEFAULT_HYPERTERMINAL_UART_ID XPAR_PS7_UART_1_DEVICE_ID  //!< macro used to abstract Physical Port of Hyperterminal UART
 #define DEFAULT_HYPERTERMINAL_UART_ADDRESS XPAR_PS7_UART_1_BASEADDR
 
**4** - commented function **led_knight_rider** inside **MaximPmod.c** file to obtain application fast start.

::

 // Toggle the LEDs so that the user knows the board is awake
	XGpio_Initialize(&g_xGpioLed, XPAR_AXI_GPIO_LED_DEVICE_ID);
	XGpio_SetDataDirection(&g_xGpioLed, 1, 0x00000000); // Set the LED peripheral to outputs
 // 	led_knight_rider(&g_xGpioLed,2);     <----
 
**5** - changed costant definition **ABOUT_ONE_SECOND** inside **MaximPmod.h** file as follow:

::

 #define ABOUT_ONE_SECOND 74067512/8   <----
 //#define ABOUT_ONE_SECOND 74067512      //!< approx 1 second delay when used as argument with function delay(numberCyclesToDelay)
 // Update this if uBlaze/Zynq CPU core frequency is changed, or if the external memory timing changes.
 // Although emprirically tested to 1.0000003 seconds, it is not meant to be used for precise timing purposes
	
**6** - improved definition inside "utilities.h", row 103, as follow

::

 void set_seven_segment_character(u8 uchDigitNumber, u8 uchValue, u8 uchDecimalActive);
 void print_seven_segment_number(float fNumber);
 extern struct maximDateTime *t;  //NEEDED FOR MQX CORRECT BUILD  <----
 //struct maximDateTime *t;
 void print_seven_segment_time(struct maximDateTime *t);	
 
**7** - changed triangle wave ramp value for MAX5216 (file menu.c, row 765 anf 769)

::
	
			case 12:
				printf("Triangle Wave started\r\n");
				fflush(stdout);
				for(i=0;i<300;i++)
				{
 //					for(j=0;j<65535;j=j+23)
					for(j=0;j<65535;j=j+230)     <-- new ramp definition
					{
						max_MAX5216_set_output_voltage(g_pActiveGPIOPort,j);
					}
 //					for(j=65535;j>=0;j=j-23)
					for(j=65535;j>=0;j=j-230)	<-- new ramp definition
					{
						max_MAX5216_set_output_voltage(g_pActiveGPIOPort,j);
					}
				}
				nMenuState = 0;
				break;

				
**NOTE: All these changes are tested on revision 1.6 of Maxim project files and need to be checked on further new revisions**
