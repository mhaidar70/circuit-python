# CircuitPython
Directory of all students! (https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello CircuitPython](#Hello_CircuitPython)
* [CircuitPython Servo](#CircuitPython_Servo)
* [CircuitPython LCD](#CircuitPython_LCD)
* [Motor Control](#Motor_Control)
* [Temperature Sensor](#Temperature_Sensor)
* [Rotary Encoder](#Rotary_Encoder)

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
I didn't have any problems with this assignment because it was an easy one. My mind got refreshed and I remembered how to do Engineering stuff.




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

code for the servo to spin around and around
### Evidence

![Servo_Code_GIF](https://user-images.githubusercontent.com/112962044/196994088-11661c96-7e4b-451e-98c3-4536bcc83a99.gif)
   
 Gif Credit goes to Cyrus (https://github.com/cwyatt29/CircutPython)
### Wiring
![image](https://user-images.githubusercontent.com/112962044/196994546-1cc2e3e9-80b0-4736-b569-d185ac06a4dc.png)

Yellow goes to a third pin on th esrvo and a pin on the board, and red goes to middle pin on the servo and 5V to the board, and brown goes to the first and GND.
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
Code for the LCD 
### Evidence


https://user-images.githubusercontent.com/112962044/197225605-ef2e2c80-1eee-4576-9795-3a2e115f52c0.mp4

Video of the LCD changing values

### Wiring
![image](https://user-images.githubusercontent.com/112962044/197226060-e3298a90-a974-482b-9369-7a12bdccdef5.png)

Pretty easy wiring as long as it's followed correctly.
### Reflection
I had a few problems with this assignment as I usually do. One of them was that I didn't have the neccessary libraries downloaded and installed into my circuit python library. I found this out when it kept saying that an import line is wrong or not working and that was because the library didn't even exist in the circuit python's  inventory. After I got the right ones, then the wrong part of the code worked well. Also another mistake to learn from was that I didn't read the instructions carefully. I got this code then uploaded it and it worked but what I didn't remember to do was to get the button to get the value that was shown on the LCD to change. When I changed the switch then it would count up or down based on the postition of the switch. I only got it to increase the value but it wasn't going down, so I had to edit my code. So I added value variable which was what the number was written on the LCD, and change variable was what would make the value increase or decrease. So  to sum it all up, I need to pay extra attention to the instructions and make sure that I have completed all the requirements.




## CircuitPython Distance Sensor.

### Description & Code

We had to use a ultrasonic sensor to change the color of the neopixel on the Metro board based on the how far it was from an object.

```python
import time
import board
import neopixel
import adafruit_hcsr04
import simpleio                     #imported lib

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D11, echo_pin=board.D12)
dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.2               #setting up ultrasonic and neopixel   .

while True:
    try:
        cm=int(sonar.distance)      #defining cm as a variable of what the ultrasonic sensor is reading
        print(cm)
        if cm<5: 
            dot.fill((255, 0, 0))   #if the distance is less than 5 cm, red
            time.sleep(.15)
        elif 5<=cm<20:
            red=simpleio.map_range(sonar.distance,5,20,255,0)
            green=simpleio.map_range(sonar.distance,5,20,0,0)
            blue=simpleio.map_range(sonar.distance,5,20,0,255)
            dot.fill((red,green,blue))                   #smoothly trasition from red to blue as the distance goes from 5cm to 20cm
            time.sleep(.05)
        elif 20<=cm<=35:   
            red=simpleio.map_range(sonar.distance,20,35,0,0)
            green=simpleio.map_range(sonar.distance,20,35,0,255)
            blue=simpleio.map_range(sonar.distance,20,35,255,0)
            dot.fill((red, green, blue))                 #smoothly trasition from blue to green as the distance goes from 20cm to 35cm
            time.sleep(.05)
        elif cm>35:
            dot.fill((0, 255, 0))                        #if the distance is more than 35 cm, turn the light green
            time.sleep(.15)
        else:
            dot.fill((0, 0, 0))                          #if there is no reading, off
            time.sleep(.15)
    except RuntimeError:                                 #if there is no numbers then tell me
        print("Retrying!")
    time.sleep(0.1)                                      #debounce

```
Code for the ultrasonic sensor to change colors
### Evidence


https://user-images.githubusercontent.com/112962044/197234116-0a9dd273-31cd-479e-b713-c22cf6dbfd58.mp4

Vdeo of the board changing color as the sensor moves closer and farther from the screen. 
### Wiring
![image](https://user-images.githubusercontent.com/112962044/197234381-6ed7742e-0628-4f3c-b8d1-24ea12840b43.png)

Very simple wiring of the sensor to the board

### Reflection
I made plenty of mistakes from this assignment and I'm glad I made those and now I have learned from it. I learned a new libarary and how it can help me in the future as well. What I mainly learned from this assignment was to keep trying and asking for help and having patience. I was worrying that I might not finish this ever and I'm going to get an F on it, but I had to re-collect myself and think positive that I will finish it. I had to get help from a few friends and learned from them. But most importantly, I shouldn't stress too much about the assignments. If I use what I learned and try my best, and especially get help from other sources can really make things faster and easier for me. It was getting me frustrated about not being able to finish it, but in the end I made it through.


## Motor_Control

### Description and Code
This assignment had us to increase or decrease a motor's power using a potentiometer.


```python
import time
import board
import analogio

# we're going to use a potentiometer to control the speed of a motor, no motor controller is used.

#Variables for analog in, for the pot... analogOUT
potentiometer = analogio.AnalogIn(board.A5)  # potentiometer connected to A1, power & ground
motor = analogio.AnalogOut(board.A0)


while True:
    # read the potentiometer
    motorVal = potentiometer.value
    print(motorVal)

    # write to the motor , using the pot values
    motor.value = motorVal

    time.sleep(.1)
```

### Evidence

![motor control](https://user-images.githubusercontent.com/112962044/200892691-90831f45-2461-4f91-9892-5b1d8aa2d0e1.png)




https://user-images.githubusercontent.com/112962044/200897575-1eedadb5-9949-48f6-a680-13e5e5f80b88.mov




## Reflection

I learned a very useful thing about wiring, and that is to keep it neat. Make one side of the board an circuitpython side and the other side make it like a motor side. So the circuit python side would have things that have to do with a lot of wiring and code, and the other side will have the wiring for the motor. This way the board looks neater and our brain can see it from a clean persepective and complete the assignment easily. A new idea that I learned from Mr. H was to write the comments first then the codes. Write the stuff it needs like "read potentionmeter" then I would figure out what the code would be to read the potentiometer. This was a very easy and effective way the we got the motor to  move the way we wanted it to move. 

## Temperature Sensor

### Description and Code
I had to code a TMP36 sensor to tell me the temperature and if it's between a certain interval it will show on the LCD if it's too hot, too cold, or just right. 


```python
import board
from lcd.lcd import LCD # lcd libraries
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import analogio
import simpleio # map library
import time

i2c = board.I2C() # lcd declaration
lcd = LCD(I2CPCF8574Interface(i2c, 0x3f), num_rows=2, num_cols=16)

tempSensor = analogio.AnalogIn(board.A0) # connects temp sensor

temp = 74 # temperature
oldTemp = 0 # reload variable
message = " "

while True:
    temp = int(simpleio.map_range(tempSensor.value,0,65535,32,212)) # maps values to Fahrenheit
    if (oldTemp != temp): # checks if needs to reprint lcd text
        if (temp <= 66): # if temp lower than 70
         message = "Too cold!"
        elif (temp >= 66): #if temo  higher than 70
            message = "Too hot!"
        else: # if temp 60-65
            message = "Just right"
        lcd.clear()
        lcd.set_cursor_pos(0,0)
        lcd.print(str(temp)) # prints temp
        lcd.set_cursor_pos(0,3)
        lcd.print("deg F")
        lcd.set_cursor_pos(1,0)
        lcd.print(message)
    oldTemp = temp
    time.sleep(1)
 ```

### Wiring and Evidence

![image](https://user-images.githubusercontent.com/112962044/227573108-f252c33a-947a-4217-ad08-97de725233bd.png)

https://user-images.githubusercontent.com/112962044/227572134-3823a69d-66df-447f-b77f-0b2329b0b792.mov

## Reflection

For this assignment I used a normal switch to control the power of the LCD because it was sucking up too much power so it was in the way of the code to run to the board. To fix this, we used a breadboard switch which is very useful and great. Of course, I didn't know what it was but I asked the teacher and learned to use breadboard switch.

## Rotary Encoder

### Description and Code 


```python
import board
from lcd.lcd import LCD # lcd libraries
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import rotaryio # rotary encoder library
import digitalio # led library
import time

i2c = board.I2C() # lcd declaration
lcd = LCD(I2CPCF8574Interface(i2c, 0x3f), num_rows=2, num_cols=16)

encoder = rotaryio.IncrementalEncoder(board.D3,board.D4) # rotary potentiometer

button = digitalio.DigitalInOut(board.D2) # rotary  button
button.pull = digitalio.Pull.UP
button.direction = digitalio.Direction.INPUT

stop = digitalio.DigitalInOut(board.D8) # red LED
stop.direction = digitalio.Direction.OUTPUT

caution = digitalio.DigitalInOut(board.D9) # yellow LED
caution.direction = digitalio.Direction.OUTPUT

go = digitalio.DigitalInOut(board.D10) # green LED
go.direction = digitalio.Direction.OUTPUT

position = 0 # starting position
states = ["stop", "caution", "go"] # states
state = " " # lcd print state
x = 0 # array selection

while True:
    prestate = state #  reprint
    position = encoder.position % 20 # finds ticks from 0
    if (position < 7): # if stop
        x = 0
    elif (position > 12): # if go
        x = 2
    else: # if caution
        x = 1
    state = states[x] # sets state
    if (button.value == False): # if button is pressed
        stop.value = False
        caution.value = False
        go.value = False
        if (state == "stop"): # turns on light
            stop.value = True
        elif (state == "caution"):
            caution.value = True
        else:
            go.value = True
    if (state != prestate): # reprints LCD data
        lcd.clear()
        lcd.set_cursor_pos(0,0)
        lcd.print("Push for ")
        lcd.set_cursor_pos(0,9)
        lcd.print(state) # prints state of rotary encoder
    time.sleep(0.1)
    
 ```
    
  ### Wiring and Evidence
  ![Screenshot 2023-03-28 105222](https://user-images.githubusercontent.com/112962044/228278530-710a00f3-a6ad-4c74-bc69-2cddacc49353.png)


https://user-images.githubusercontent.com/112962044/228279418-8cf198ad-c0ef-44f6-9719-9b9fa2b3d17e.mov

## Reflection
The rotary encoder is a really useful tool to use in Engineering. Before it can be useful, it needs to have probems of course. For this assignment I had the correct wiring off the slideshow but the rotary enocder was not changing the color at all. The code was looking good as if it had no prolems or so I thought. I double checked my wiring on all of the stuff, but it was good. So that meant it was the code, I kept on looking through until I found the problem, the pins. I had wrote the wrong pins so it was not sending any signal through the encoder. I fixed the pins on the code and voila! It was up and running perfectly. So moral of story: check pins on board and the code because that could save you a lot of time. 

