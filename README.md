# THE DIMMER_M4SDRV_V1
Linear BLDC motor controller with TMC2209 for rotation dev. based on SAMD(E)51 MCU. The primary goal of this project is to make a linear motor controller, which can control the (single or multiple) Z axis and rotation on openPnP machines. With that said, the hardware could be used to control other (sub 10amp) 3 phase motors or steppers. In the openPnP community, there has been development on multi-nozzle machines for some time. This is an attempt to simplify and specify the hardware for openPnP machines.

By introducing sub-controllers in openPnP, it is now possible to delegate various tasks to various controllers. This project builds on that feature. Each z-axis subcontroller, will connect to the mainframe by either USB or CAN

Files are made with Kicad Nightly Build. If you have the latest stable releace installed, you can install the Nightly build next to it in eg. KicadNightly folder. Just dont install systam variables, which is chosen in the install guide.

![TOP](https://github.com/Juanduino/THE-DIMMER_M4SDRV_V1/blob/master/Images/TOP.PNG)
 
PROS: 

By using a linear 3 phase motor controller with an onboard stepper IC for rotation, wires can be kept very short.
 
The linear motor is easy to make yourself with common 3mm long neodymium magnets. (Onboard Hall sensors is spaced apart, with the appropriate distance for these magnets). Likewise a external (angle)sensor can be connected via SPI, I2C or Serial.
 
To make the motor, the idea is to fill up a eg. stainless steel pipe with magnets and spacers between those magnets. The coils of the motor will be wound on a 3D printed "slider" (bushing) with the appropriate spacing to match the magnet's length (3mm).
 
By winding the coils around the magnets, the entire pull/push of the magnets is used and the linear motor is not as sensitive to the distance between coils and magnets.
 
The south and north pole of the coils will be in the direction of movement, unlike normal BLDC motors, where you make two windings for each pole pair.
 
Mosfets have quite different specs. when it comes to voltages and current ratings. If using 12v or 24v for a motor, its better to use 30v rated mosfets with a much lower Rds(on) (resistence) compared to higher voltage rated MOSFETS. 
The amount of heat dissipated from the Mosfets can be calculated. (see page 3 https://d1d2qsbl8m0m72.cloudfront.net/en/products/databook/applinote/ic/power/switching_regulator/power_loss_appli-e.pdf)

CONS: It takes time to perfect. All good cookies take time to make. The intended Arduino Library (SimpleFoc) needs further development to be able to work with inline current sensing.

Changelog:

Added MAX40056 Current sensor on 3 out of 4 phases. The last fase will have to follow one of the ones with sensor if used seperately. In stepper configuration, the sensor will monitor the two windings on two bidirectional sensors.
In 3 phase configuration, the 3 current sensors will be in use. The MAX40056 has advanced PWM rejection, and ultra fast settle time. This ensures a good read in harsh PWM invironments.

Added MOSFET driver MIC4605-2 which control high side & Low side using one PWM input. This mean we can use the SimpelFOC lib. as is (Current sense still need implementation).
This driver is not just fast its totally fast. Combined with the ultra low Gate charge and rise/fall time of the Infinion Mosfets, hopefully this will keep things cool.
 
Note: Adafruit is adding support for SAME51, which has native CAN FD support.
(source: https://github.com/adafruit/ArduinoCore-samd/pull/267)

HARDWARE:

SAME51 MCU 120 mhz M4 architecture with CAN FD (https://www.microchip.com/wwwproducts/en/ATSAME51J20A)

TMC2209 stepper driver (https://www.trinamic.com/products/integrated-circuits/details/tmc2209-la/)

MOSFETS BSC0925ND Dual channal 40amp 17nC gate charge (https://www.infineon.com/cms/en/product/power/mosfet/12v-300v-n-channel-power-mosfet/bsc0925nd/)

Gate drivers MIC4605-2 PWM indput (https://www.microchip.com/wwwproducts/en/MIC4605)

Current sensors MAX40056 (https://datasheets.maximintegrated.com/en/ds/MAX40056F-MAX40056U.pdf)

Step-Down converter 4v/36v to 10v rail 1amp (https://www.ti.com/product/LMR50410)

3.6v LDO 500mA (https://ww1.microchip.com/downloads/en/DeviceDoc/MIC5219-500mA-Peak-Output-LDO-Regulator-DS20006021A.pdf)

3 x ANALOG HALL sensors (https://www.ti.com/product/DRV5053?qgpn=drv5053). 

Analog hall sensors will potentially give a precision of the ADC resolution over one polepair. Thats 12bit (4096:1) (3mm/4096=0,0007mm)


Communication ports:

SERCOM port can be configuered to I2C, SPI and serial.

CAN FD is integrated into the SAME51 MCU.

USB 2.0 full speed. (USB port data-pins is broken out)




 

