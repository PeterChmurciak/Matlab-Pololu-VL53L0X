# Matlab Pololu VL53L0X

Matlab add-on that allows Matlab to receive data from the VL53L0X distance sensor through an Arduino board. It is based on [Pololu library](https://github.com/pololu/vl53l0x-arduino) and was inspired by [similiar add-on](https://github.com/sandorcourane/matlab-vl53l0x) that uses [Adafruit library](https://github.com/adafruit/Adafruit_VL53L0X).

## How to install
To be able to work with Arduino in Matlab you have to have [MATLAB Support Package for Arduino](https://www.mathworks.com/hardware-support/arduino-matlab.html) installed. 

Assuming you have installed it already, for the add-on to work, the [Pololu library](https://github.com/pololu/vl53l0x-arduino) has to be included in your Arduino libraries folder. Pololu library file is named `vl53l0x-arduino-master` and it needs to be included in the folder with default path `C:\Users\YourPC\Documents\Arduino\libraries`. This can be done manually by simply moving the file there, or by including the .zip library file through [Arduino IDE](https://www.arduino.cc/en/Guide/Libraries#toc4). 


To use this add-on you have to copy the `+arduinoioaddons` file somewhere on your computer and 
add it to the Matlab search path. 

For example if its current location is `C:\Program Files\myProject\myFile\+arduinoioaddons` you would use Matlab command `addpath('C:\Program Files\myProject\myFile')`.

Now Matlab should be able to recognize the Arduino library inside of this add-on. To check if was detected sucessfully use Matlab command
`listArduinoLibraries`.

You should see the `{'Pololu/Pololu_VL53L0X'}` somewhere in the list of listed libraries.

## How to use

* Firstly, you have to create arduino object in Matlab. For example if you are using Arduino UNO, it is connected to COM3 and you want to use this library on it, then command to create this object would look like:

    `arduinoObject = arduino('COM3', 'Uno', 'Libraries', 'Pololu/Pololu_VL53L0X')`
 
 * The next thing you need to do, is to create sensor object in Matlab. Sensor object is linked to arduino object and its creation should look like:
 
    `sensorObject = addon(arduinoObject, 'Pololu/Pololu_VL53L0X')`    

* After that comes initialisation of the sensor with:
    
    `beginSensor(sensorObject)`

* Getting readings from sensor with:

    `readingInMillimetres = readSensor(sensorObject)`
    
* And in case you do not need it anymore, removing the sensor object with:
    
    `removeSensor(sensorObject)`
    
## Note

The add-on uses continuous reading mode with 20 millisecond measure timing budget. To modify the timing budget and/or add more functions to the add-on see the functions of the library it uses - [Pololu library functions](https://github.com/pololu/vl53l0x-arduino#library-reference).
