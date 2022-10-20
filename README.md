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
xel](https://user-images.githubusercontent.com/112962044/196989630-ae9feee7-803e-4c8f-96a5-2e356e2bec94.jpg)


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
I had one problem with writing the pin for the servo. I didn't know that you had to put a dot and write a D for analog pins so I learned that. For example, I plugged the servo in pin 2, so I had to write D2. to command it on pin 2. 


## CircuitPython_LCD

### Description & Code

```python
Code goes here

```

### Evidence

Pictures / Gifs of your work should go here.  You need to communicate what your thing does.

### Wiring

### Reflection





## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection
