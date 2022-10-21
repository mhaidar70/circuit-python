# CPyProjectTemplate
These are the projects and assignments we work on in Engineering class.
# CircuitPython
This repository will actually serve as a aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [NextAssignmentGoesHere](#NextAssignment)
---

## Hello_CircuitPython

### Description & Code
I coded for the board to say hi on the serial monitor.

```python
from time import sleep

while True:
    print("Hi")
    sleep(1)   
```


### Evidence
![circuitpython_Cat_code_py_Hello_World](https://user-images.githubusercontent.com/112962044/196995655-90f2caa2-a835-4448-9f52-2849d2f1b054.png)


Image credit goes to [Adafruit](https://learn.adafruit.com/getting-started-with-raspberry-pi-pico-circuitpython/circuitpython-programming-basics)



### Wiring
![Screenshot 2022-10-20 112152](https://user-images.githubusercontent.com/112962044/196990545-22f2c92a-532f-4ee6-b455-92e79ca538ed.png)
 
 Wiring is really simple just plug in a USB wire to the board and the computer.

### Reflection
I didn't have any problems with this assignment because it was an easy one.




## CircuitPython_Servo

### Description & Code
I coded a 180 degrees servo to turn and spin around and around. 

```python
import time
import board
import pwmio
from adafruit_motor import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.D2, duty_cycle=2 ** 15, frequency=50)
# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.0001)
    for angle in range(180, 0, -5): # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)

```

### Evidence

![Servo_Code_GIF](https://user-images.githubusercontent.com/112962044/196994088-11661c96-7e4b-451e-98c3-4536bcc83a99.gif)
   
 Gif Credit goes to Cyrus (https://github.com/cwyatt29/CircutPython)
### Wiring
![image](https://user-images.githubusercontent.com/112962044/196994546-1cc2e3e9-80b0-4736-b569-d185ac06a4dc.png)

### Reflection
I had one problem with writing the pin for the servo. I didn't know that you had to put a dot and write a D for analog pins so I learned that. For example, I plugged the servo in pin 2, so I had to write .D2, to command it on pin 2. 


## CircuitPython_LCD

### Description & Code

```python
import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
from digitalio import DigitalInOut, Direction, Pull 

#sets buttons and switch as Inputs 
btn= DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn.pull = Pull.DOWN
switch = DigitalInOut(board.D10)
switch.direction = Direction.INPUT
switch.pull = Pull.UP

# get and i2c object
i2c = board.I2C()

# some LCDs are 0x3f... some are 0x27.
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)

value = 0 #sets the value to 0 to count up from there
change=1 #variable used to change value
SwitchState = switch.value

lcd.print("Button:") 
lcd.set_cursor_pos(0,8) #sets position of the LCD in the 2 by 16 grid

prev_state = btn.value

while True: #sets button to add up and not count when held down
    cur_state = btn.value
    if cur_state != prev_state:
        if not cur_state:
            value = value + change
            lcd.set_cursor_pos(0,8)
            lcd.print(str(value))
    if switch.value == True: # prints switch is up if switch value is true
      lcd.set_cursor_pos(1,0)
      lcd.print("Up  ")
      change = 1 #increases value
    else: #if the switch isn't true then it prints "down"
      lcd.set_cursor_pos(1,0) 
      lcd.print("Down")
      change = -1 #decreases value
    prev_state = cur_state
  


```

### Evidence


https://user-images.githubusercontent.com/112962044/197225605-ef2e2c80-1eee-4576-9795-3a2e115f52c0.mp4



### Wiring
![image](https://user-images.githubusercontent.com/112962044/197226060-e3298a90-a974-482b-9369-7a12bdccdef5.png)

### Reflection
I had a few problems with this assignment as I usually do. One of them was that I didn't have the neccessary libraries downloaded and installed into my circuit python library. I found this out when it kept saying that an import line is wrong or not working and that was because the library didn't even exist in the circuit python's  inventory. After I got the right ones, then the wrong part of the code worked well. Also another mistake to learn from was that I didn't read the instructions carefully. I got this code then uploaded it and it worked but what I didn't remember to do was to get the button to get the value that was shown on the LCD to change. When I changed the switch then it would count up or down based on the postition of the switch. I only got it to increase the value but it wasn't going down, so I had to edit my code. So I added value variable which was what the number was written on the LCD, and change variable was what would make the value increase or decrease. So  to sum it all up, I need to pay extra attention to the instructions and make sure that I have completed all the requirements.




## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection
