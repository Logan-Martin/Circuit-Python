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

```python
print("This is main.Py and HELLO!!!")
```
### Evidence
![image of code working printing stuff](https://user-images.githubusercontent.com/71342159/133098796-1837352f-285e-4320-9fa0-68d2ef830ce1.png)

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

<img src="https://user-images.githubusercontent.com/71342159/133619724-9c6e58cb-32ec-4157-b4d0-c997c9996b8c.gif" width="250" height="250" />

### Reflection
I have become better at coding with ciruit python. So far everything has been changing other people's code and failing at writing my own, but I am learning. 9/13/2021.



## CircuitPython_LCD

### Description & Code

The code bellow counts up numbers and counts down when you touch the blue wire. Like a switch. The red wire will either count up or down depending on the blue wires "mode". The LCD will show if it is counting up or down.

```python
import time
import board
import digitalio
import adafruit_character_lcd.character_lcd as characterlcd
import pwmio
import touchio

# Modify this if you have a different sized character LCD
lcd_columns = 16
lcd_rows = 2

# Metro M0/M4 Pin Config:
lcd_rs = digitalio.DigitalInOut(board.D7)
lcd_en = digitalio.DigitalInOut(board.D8)
lcd_d7 = digitalio.DigitalInOut(board.D12)
lcd_d6 = digitalio.DigitalInOut(board.D11)
lcd_d5 = digitalio.DigitalInOut(board.D10)
lcd_d4 = digitalio.DigitalInOut(board.D9)
lcd_backlight = digitalio.DigitalInOut(board.D13)

# Initialise the LCD class
lcd = characterlcd.Character_LCD_Mono(
    lcd_rs, lcd_en, lcd_d4, lcd_d5, lcd_d6, lcd_d7, lcd_columns, lcd_rows, lcd_backlight
)

touch_pad = board  # Will not work for Circuit Playground Express!

touch = touchio.TouchIn(touch_pad.A0)
touchTwo = touchio.TouchIn(touch_pad.A1)

testValue = 0

a = 0
b = 1

goUpInValue = 1
valueHasChangedOnceAlready = 0

# This is how you turn on the backlight: ( lcd.backlight = True )

# How to Print a two line message: ( lcd.message = "Hello\nCircuitPython" )

# How to do a Wait: ( time.sleep(5) )

# This clears the text off the LCD screen: ( lcd.clear() )

# How to Print two line message right to left ( Flipping the text ):  ( lcd.text_direction = lcd.RIGHT_TO_LEFT ) and ( lcd.message = "Hello\nCircuitPython" ) on the line bellow the first one
# /n makes a new line on the LCD

# How to Return text direction to left to right ( Flipping the text to the normal way ): ( lcd.text_direction = lcd.LEFT_TO_RIGHT )

# How to Display cursor ( lcd.cursor = True ) and make a print so you can see it better. ( lcd.message = "Cursor! " )

# How to make cursor blink ( lcd.blink = True ) and make a print to make it make more sense ( lcd.message = "Blinky Cursor!" ) Make sure the cursor is displayed first.

# Create message to scroll ( scroll_msg = "<-- Scroll") make a line bellow and put this: (lcd.message = scroll_msg )
# this is how you make the message scroll across the screen:
#   for i in range(len(scroll_msg)):
#    time.sleep(0.5)
#    lcd.move_left()

# Turn backlight off ( lcd.backlight = False )

while True:
    time.sleep(.05)
    if touch.value:
        if goUpInValue == 1:
            lcd.clear()
            a = a + b
            print(a)
            lcd.message =  "\nGoing up:"
            lcd.message = str(a)
        if goUpInValue == 0:
            lcd.clear()
            a = a - b
            print(a)
            lcd.message =  "\nGoing down:"
            lcd.message = str(a)

    if touchTwo.value:
        print("Touched blue wire")
        if valueHasChangedOnceAlready == 0:
            if goUpInValue == 1:
                valueHasChangedOnceAlready = 1
                goUpInValue = 0
                
        if valueHasChangedOnceAlready == 0:
             if goUpInValue == 0:
                valueHasChangedOnceAlready = 1
                goUpInValue = 1


    if valueHasChangedOnceAlready == 1:
        time.sleep(1)
        valueHasChangedOnceAlready = 0


```

### Evidence

<img src="https://github.com/Logan-Martin/Circuit-Pyth0on/blob/main/ezgif-3-6dded6828d3a.gif" width="250" height="250" />

### Reflection

Making this at first was a bit annoying as I had a different library than most people. I feel like learning from libraries is very confusing at times, api and google help a ton though.

## CircuitPython Photointerrupters

### Description & Code

```python
Code goes here

```

### Evidence


### Reflection
