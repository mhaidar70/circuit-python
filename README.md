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
I coded for the board to change the neopixel color to red

```python
import board
import neopixel

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.5 

print("Make it red!")

while True:
    dot.fill((255, 0, 0))   
```


### Evidence
![circuitpython_CLUE_Badge_red_neopixel](https://user-images.githubusercontent.com/112962044/196989630-ae9feee7-803e-4c8f-96a5-2e356e2bec94.jpg)


Image credit goes to [Adafruit](https://learn.adafruit.com/clue-custom-circuit-python-badge/pybadger-colors)



### Wiring
![Screenshot 2022-10-20 112152](https://user-images.githubusercontent.com/112962044/196990545-22f2c92a-532f-4ee6-b455-92e79ca538ed.png)
 
 Wiring is really simple just plug in a USB wire to the board and the computer.

### Reflection
I accidentally wrote the wrong RGB value for blue when I actually needed red. So I got a bad grade then I learned to fix the value and make sure it's correct. 




## CircuitPython_Servo

### Description & Code

```python
Code goes here

```

### Evidence

Pictures / Gifs of your work should go here.  You need to communicate what your thing does.

### Wiring

### Reflection




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
