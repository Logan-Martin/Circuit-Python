# CircuitPython
 The follwing files are my first foray into CircuitPython.
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [NextAssignmentGoesHere](#NextAssignment)
---

## Hello_CircuitPython

### Description & Code
Description goes here

Here's how you make code look like code:

```python
print("This is main.Py and HELLO!!!")
```
### Evidence
![image of code working printing stuff](https://user-images.githubusercontent.com/71342159/133098796-1837352f-285e-4320-9fa0-68d2ef830ce1.png)

### Images
Make an account with your google ID at [tinkercad.com](https://www.tinkercad.com/learn/circuits), and use "TinkerCad Circuits to make a wiring diagram."  It's really easy!  
Then post an image here.   [here's a quick tutorial for all markdown code, like making links](https://www.markdownguide.org/basic-syntax/)

### Reflection
I have been confused on how to accually run a file on the metro 0 board for 2 weeks. I finally got it to run on my own by deleting all .py files but main.py, reset my board, and printed code on main.py. I still don't know exactly how it works as of 9/13/2021.


## CircuitPython_Servo

### Description & Code

```python
import time
import board
import pwmio
from adafruit_motor import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

print("working")

while True:
    for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
        print("moved")
    for angle in range(180, 0, -5): # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)

```
Spicy version:
```python
from adafruit_motor import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

touch_pad = board  # Will not work for Circuit Playground Express!

touch = touchio.TouchIn(touch_pad.A0)
touchTwo = touchio.TouchIn(touch_pad.A1)

testValue = 0


while True:
    if testValue >= 180:
        testValue = 90

    if testValue <= 0:
        testValue = 90
    
    
    if touch.value:
        print("move left!")
        my_servo.angle = testValue
        testValue = testValue + 10
        time.sleep(0.05)
    time.sleep(0.05)
    
    if touchTwo.value:
        print("move right!")
        my_servo.angle = testValue
        testValue = testValue - 10        
        time.sleep(0.05)

    time.sleep(0.05)
```

### Evidence
Youtube Video of the Servo Code Working: https://www.youtube.com/watch?v=Zwhp-15UYDY

### Images
![image of servo](https://user-images.githubusercontent.com/71342159/133262278-f83a713a-2d46-486a-9fe9-013440e6b799.png)


### Reflection
I have become better at coding with ciruit python. So far everything has been changing other people's code and failing at writing my own, but I am learning. 9/13/2021.



## CircuitPython_LCD

### Description & Code

```python
Code goes here

```

### Evidence

### Images

### Reflection





## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Images

### Reflection
