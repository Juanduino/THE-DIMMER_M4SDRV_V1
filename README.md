# THE DIMMER_M4SDRV_V1
Linear BLDC motor controller with TMC2209 for rotation dev. based on SAMD(E)51 MCU. The primary goal of this project is to make a linear motor controller, which can control the (single or multiple) Z axis and rotation on openPnP machines. With that said, the hardware could be used to control other (sub 10amp) 3 phase motors or steppers. In the openPnP community, there has been development on multi-nozzle machines for some time. This is an attempt to simplify and specify the hardware for openPnP machines.

By introducing sub-controllers in openPnP, it is now possible to delegate various tasks to various controllers.This project builds on that feature. Each z-axis subcontroller, will connect to the mainframe by either USB or CAN

Files are made with Kicad Nightly Build.
 
PROS: 
By using a linear 3 phase motor controller with an onboard stepper IC for rotation, wires can be kept very short.
 
The linear motor is easy to make yourself with common 3mm long neodymium magnets. (Onboard Hall sensors is spaced apart, with the appropriate distance for these magnets)
 
To make the motor, the idea is to fill up a eg. stainless steel pipe with magnets and spacers between those magnets. The coils of the motor will be wound on a 3D printed "slider" (bushing) with the appropriate spacing to match the magnet's length (3mm).
 
By winding the coils around the magnets, the entire pull/push of the magnets is used and the linear motor is not as sensitive to the distance between coils and magnets.
 
The south and north pole of the coils will be in the direction of movement, unlike normal BLDC motors, where you make two windings for each pole pair.
 
CONS: It takes time to perfect. All good cookies take time to make. The intended Arduino Library (SimpleFoc) needs further development to be able to work with current sensing and 6 pin switch control, which will be SAMD(E)51 specifik.

 
This hardware project is licensed under the Creative Commons CC-BY-NC-SA 
https://creativecommons.org/licenses/by-nc-sa/4.0/
 
(That is, you are free to use this hardware repo for personal use, but if you want to sell the hardware, a agreement between the author and yourself/legal party is mandatory).


