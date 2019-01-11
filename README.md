# Swarm Bots

Repository for the hardware and software of a swarm robotics project.

## Design Requirements

* Inexpensive
* High level of accuracy for motor control
* Accurate distance measurements and global positioning
* Wireless communication with host computer
* Testbed for conducting sensor calibration and testing
* Needs to be able to be assembled by hand soldering or with a reflow oven
* As small a footprint as possible
* Charging station for easy recharge

## Convenience Features

* Automatic senor calibration
* Automatic battery charging
* Wireless programming
* Local communication between bots

## Design Breakdown

### Simplicity and Extensability

* Modular design - layers can be removed and added to the design

### Low cost

* Most expensive singular componants are likely to be the motors and battery pack
* Need to find low cost options for both of these to make the project feasable

### Small form factor

* Limit footprint to approx. 30x30mm

### Useability

* Collective programming, powering and charging, and control
* Automatic sensor calibration

GRITSBOT example: EEPROM chip enables wireless prgramming of both motor board and main board
in a addition to individually  reprogramming a robot based on its unique wireless ID, it is also possible to broadcast reprogram all available robots or groups of robots

### Design

* Layered design (layers can be replaced / upgraded without distrupting the functionality of the other layers)
* Example Layers:
  * Motorboard (lowest layer) - needs motor mcu, motors (pobably on bottom of board), motor controller
  * Main borad (middle layer) - main mcu, battery charger, voltage regulator
  * Sensor board (top board) - contains IR distance sensors, IMU (accelerometer and gyro)

### Locomotion

* Most likely use micro DC motors, inexpensive examples below: 
https://au.element14.com/multicomp/mm18/motor-miniature-1-5-4-5v-6-8krpm/dp/599116
https://au.element14.com/multicomp/mm28/motor-miniature-3-6v-9600rpm/dp/599128
https://au.element14.com/multicomp/mm10/motor-miniature-1-5-3-0v-16-3krpm/dp/599104
https://au.element14.com/adafruit-industries/711/hobby-dc-motor-6vdc-9100rpm/dp/2457411
  * Note: will need motor encoder to estimate velocity
* Alternatively consider vibration control or stepper motor

### Sensing

* Most common distance sensing in swarm bots is IR
* Measurements of distances and bearing to neighbouring bots and obsticals can be done with IR
* Accellerometer and gyroscope (IMU)
* Battery voltage sensor - inform control of recharge behaviour

### Communication

* RF transcever most viable option and it has far lower power consumption than wifi e.g. 16mA vs 250mA
* Tradoff is a lower datareate of about 2 Mbit/s

### Processing

* 2 mircrocontrollers
* Main borad - wireless communication, sensor data processing, user defined tasks
* Motor board - motor velocity, control of motors

### Power System

* Sensor and motor boards are powered through header pins from the main board
* All battery charging circuitry is done on the main board, along with power regulation
* Bot powered by LiPo battery (will propably need voltage regulation)
* Need to do calcs to determine Ah and Voltage required

### Testbed

* Responsible for calibration
  * Example senario: move an obstical back and forth across a testbed with a known distance to calibrate a single ir sensor
  * Calibration data should be stored in EEPROM (non-volitle memory)
* Charging station
  * Example: 2 copper prongs (5V and GND) that connected to a charged wall or material (aluminium)
* The testing area can be used to aid in global positioning (with use of external camera etc.)

### Known restrictions

* Number of bots limited by bandwidth of RF channels

### Software

* All base code for bot behaviour and communication will be done in C
* Might look at using higher level language for test senarios and for making a program on computer that recieves the data from the bots