# ArduinoPixyAndRoboRIO
This is not a complete robot but rather just the code needed for the robot, Pixy camera, and Arduino to communicate over I2C. We used an Arduino Uno and the original Pixy, although we have a Pixy2 for 2019. Also for 2019 we have switched Arduinos to the [RIOduino](http://www.revrobotics.com/rev-11-1104/) from REV. The RIOduino is Arduino Uno compatible and plugs directly to the MXP port on the RoboRIO. This simplifies wire since the Arduino can now get power and communicate with the RoboRIO, including through I2C, without any other wires or mounts. 


# Arduino and RoboRIO.txt
This file contains code for the Arduino to Communicate with the RoboRIO through I2C, using the Wire library, as well as simple Pixy Code. The Pixy code looks for the biggest object on the screen matching a signature and saves it's x and y position and area to a string, which is then sent to the RoboRIO. 

The lines 
```java
String input = "blank";	 //string received from the robot
const String PIXY = "pi";
```
are not actually needed. They are simply left over lines from attempting to also use the Lidar Lite V3 with our Arduino.

# M_I2C.java
This file is where most of the code for communicating is. To actually read the data from the I2C bus you only need the few lines in the ```read``` method. If you are using the Pixy and would like to use the x,y, and area which the Arduino is currently sending then checkout the ```getPixy``` method. 

We did attempt to send data from the RoboRIO to the Arduino, in the ```write``` method, when we starting testing the Lidar Lite V3. The idea was to send a string called either "LI" or "PI" to the Arduino, hence some of the Arduino code, to tell it whether we wanted Pixy data or Lidar data. However, we struggled to get this working 100%. 

# PixyPacket.java
This is just a wrapper for the Pixy data to make it easier to use latter on.

# Credit
The code for communicating between the Arduino and RoboRIO was found on [this](https://www.chiefdelphi.com/t/need-help-with-arduino-to-i2c-on-roborio/140071/12) ChiefDelphi thread, as we struggled on it for a while. After Steamworks we stripped our code and put it in this repo to hopefully give a more complete example of a robot program using I2C.
