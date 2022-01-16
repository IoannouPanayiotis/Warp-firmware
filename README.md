# README.md file for 4B25-Coursework-5

# Summary

The aim of the project was to build an embedded system that has the 
ability to monitor water levels and give warnings when the water level reaches a critical level. 
In addition, an investigation of the power consumption of the system and the performance of the water level sensor was carried out.
The main components of the prototype are: the FRDM-KL03Z development board; an OLED (SSD1331); an Arduino water level sensor; and the INA219
sensor, which was used only to measure the power consumption of the OLED and the water level sensor. The software implementation was based
on the WARP Firmware (https://github.com/physical-computation/Warp-firmware). The diff changes can be found <a href="https://github.com/IoannouPanayiotis/Warp-firmware/pull/1/files">here</a>.
More details on the hardware and software implementation can be found below.

The system works by obtaining the current water level (using the water level sensor) every 2 seconds. When the water level of the water
is very low the OLED screen will flash green, when it is close to overfill it will flash orange and red when an overfill happens.
  
# Hardware implementation
The embedded system/prototype can be seen in the image below. On the left of the image we have the OLED on the bottom and the INA219 sensor (current/power monitor) just above the OLED. In the middle of the image we can see the FRDM-KL03Z development board and on the top right the Arduino water level sensor.
<p><img alt="Prototype" title="Prototype" src="https://github.com/IoannouPanayiotis/Warp-firmware/blob/ProjectPan1/Images%20for%20Readme/Prototype.PNG" /></p>

The circuit diagram of the main embedded system can be seen in the image below. The image also includes the connections between the pins of the FRDM-KL03Z, the OLED and the water level sensor.
<p><img alt="Circuit Diagram" title="Circuit Diagram" src="https://github.com/IoannouPanayiotis/Warp-firmware/blob/ProjectPan1/Images%20for%20Readme/Circuit%20Diagram.PNG" /></p>

In the table below we can see the pin connections between the FDRM-KL03Z development board and the INA219 sensor.
<p><img alt="Image" title="icon" src="https://github.com/IoannouPanayiotis/Warp-firmware/blob/ProjectPan1/Images%20for%20Readme/FRDM-KL03Z%20%20-%20INA219%20Wiring.jpg" /></p>  
  
# Software Implementation
<p>The code was based on the WARP firmware(https://github.com/physical-computation/Warp-firmware).
Diff against the WARP firmware can be found <a href="https://github.com/IoannouPanayiotis/Warp-firmware/pull/1/files">here:
https://github.com/IoannouPanayiotis/Warp-firmware/pull/1/files</a>
<p>


<h2>Differences to the WARP firmware</h2>
I will focus on the most important changes:    
<br/><br/>
<code><strong>adc16_Waterlevel.h<br /></strong></code>
New file. Contains the function prototypes of the functions that 
are associated with the Analog to Digital Converter (ADC).
<br/><br/>
<code><strong>adc16_Waterlevel_blocking.c<br /></strong></code>
New file. Contains the code that allows us to read an analog signal using the ADC.
Initialises the ADC converter and sets the ADC configuration (Blocking mode for my project).
Handles the conversion and outputs the ADC value in a format we can read(a number).
Includes the code that sets which colour the OLED will flash depending on the level of the water.
<br/><br/>
<code><strong>boot.c<br /></strong></code>
Most changes are just removal of code that corresponds to devices that are not used for this project.
The most important changes are included between lines 1360 and 1376. The code within these lines calls the functions
that handle all the ADC functionality.
This file also includes the changes that were made to make the INA219 sensor work within the WARP functionality.
<br/><br/>
<code><strong>CMakeLists-Warp.txt<br /></strong></code>
Included the directory path for the new files that I included in the code. I also removed most of the directories 
that pointed to files/code for devices I did not use.
<br/><br/>
<code><strong>devINA219.c<br /></strong></code>
Code to configure, read and write from the INA219 sensor. Current configuration is set to measure power. 
<br/><br/>
<code><strong>devINA219.h<br /></strong></code>
Includes the function prototypes that are associated with the INA219 sensor.
<br/><br/>
<code><strong>devSSD1331.c<br /></strong></code>
Sets up the appropriate pins in order to be able to use the OLED. Includes the functions that make the
OLED flash green, orange and red.
<br/><br/>
<code><strong>devSSD1331.h<br /></strong></code>
Includes the function prototypes and variables that are associated with the SSD1331 OLED.
