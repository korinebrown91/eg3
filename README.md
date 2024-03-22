0# CircuitPython
This repository will actually serve as an aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [NextAssignmentGoesHere](#NextAssignment)
---
## distance senser

### Description & Code
This is the Distance senser and it chages color on the distance of a hand or object.


Here's how you make code look like code:

```python
Code goes here
# SPDX-FileCopyrightText: 2021 ladyada for Adafruit Industries
# SPDX-License-Identifier: MIT

import time
import board
import adafruit_hcsr04
import neopixel

NUMPIXELS = 1  # Update this to match the number of LEDs.
SPEED = 0.05  # Increase to slow down the rainbow. Decrease to speed it up.
BRIGHTNESS = 1.0  # A number between 0.0 and 1.0, where 0.0 is off, and 1.0 is max.
PIN = board.NEOPIXEL
pixels = neopixel.NeoPixel(PIN, NUMPIXELS, brightness=BRIGHTNESS, auto_write=False)
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D7)

while True:
    try:
        print((sonar.distance,))
        if sonar.distance < 5:
            for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
                pixels[pixel] = (255, 0,0)
                pixels.show()
        if sonar.distance > 5 and sonar.distance < 20:
            for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
                pixels[pixel] = (255-(sonar.distance - 5 / 15 * 255), 0, (sonar.distance - 5 / 15 * 255))
                pixels.show()
             
        if sonar.distance > 20 and sonar.distance < 35:
            for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
                pixels[pixel] = ( 0, (sonar.distance - 5 / 15 * 255), 255-(sonar.distance - 5 / 15 * 255))
                pixels.show()
        if sonar.distance > 35:
            for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
                pixels[pixel] = ( 0, 255, 0)
                pixels.show()  
    except RuntimeError:
        print("Retrying!")
    time.sleep(0.1)

```


### Evidence
![image_67165953](https://github.com/korinebrown91/eg3/assets/75768362/ff8ea106-144a-4b68-a16c-5d7ede2d3cbc)





And here is how you should give image credit to someone if you use their work:

Image credit goes to [Rick A](https://www.youtube.com/watch?v=dQw4w9WgXcQ&scrlybrkr=8931d0bc)



### Wiring 

### Reflection
![unnamed (6)](https://github.com/korinebrown91/eg3/assets/75768362/9d224bf0-1470-4868-bf2b-a223292e9caf)
 
what went wrong was the wiring it kinda got me off graud a liittle with all wirse. Overall ever thng was good and i got the moter to move i learn that i dont have to put 5v and grd when im using my better pack. i reallylike this one because the code wont long and the wiring was hard but i got on to it quick.



## Hello_CircuitPython

### Description & Code
this is a circuitpythan and it changes the distintce of the numbers using movment 

```python
Code goes here
```python
import board
import time
import digitalio
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface

# turn on lcd power switch pin
lcdPower = digitalio.DigitalInOut(board.D8)
lcdPower.direction = digitalio.Direction.INPUT
lcdPower.pull = digitalio.Pull.DOWN

# Keep the I2C protocol from running until the LCD has been turned on
# You need to flip the switch on the breadboard to do this.
while lcdPower.value is False:
    print("still sleeping")
    time.sleep(0.1)

# Time to start up the LCD!
time.sleep(1)
print(lcdPower.value)
print("running")

i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)


# Loop forever.
while True:
```


### Evidence


![spinningMetro_Optimized](https://user-images.githubusercontent.com/54641488/192549584-18285130-2e3b-4631-8005-0792c2942f73.gif)


And here is how you should give image credit to someone if you use their work:

Image credit goes to [Rick A](https://www.youtube.com/watch?v=dQw4w9WgXcQ&scrlybrkr=8931d0bc)



### Wiring
Make an account with your Google ID at [tinkercad.com](https://www.tinkercad.com/learn/circuits), and use "TinkerCad Circuits to make a wiring diagram."  It's really easy!  
Then post an image here.   [here's a quick tutorial for all markdown code, like making links](https://guides.github.com/features/mastering-markdown/)

### Reflection 
this was a really good one for me even though i dont like wiring but went was hard for me putting the wiring in the right places on the bead bored. it took for ever for me to get it done but i feel like it got better when i was some what done and had to do the code part. i lerned that i can use new this 

What went wrong / was challenging, how'd you figure it out, and what did you learn from that experience?  Your ultimate goal for the reflection is to pass on the knowledge that will make this assignment better or easier for the next person.




## How To Fix the LCD power issue with Metro M4 boards.

### Description & Code
this is a motor control and the peice the tap is on moves it its really cool 
* **The symptoms:**  LCD acting weird OR trouble with usb connection / serial monitor / uploading / etc.
* **The problem :** The LCDs occasionally draw too much power when we turn on the boards, and that makes parts of its serial communications crash.
* **The Solution:** Add this code, and wire a switch up, like the wiring diagram below:



### Wiring

![WiringSolution](images/I2C_M4_Solution.png)
![unnamed (5)](https://github.com/korinebrown91/eg3/assets/75768362/d0b02c6c-12f6-4a21-b220-f3f8f056843b)






## Motor Control 
### Description & Code

```python
Code goes here

import board
import analogio

motor=analogio.AnalogOut(board.A0)
pot=analogio.AnalogIn(board.A1)
while True:
    speed=pot.value
    motor.value=speed
```

### Evidence

Pictures / Gifs of your work should go here.  You need to communicate what your thing does.

![image_67162881 (1)](https://github.com/korinebrown91/eg3/assets/75768362/1f77eab0-c1fb-4ae6-839c-f36c125a0b43)



### Wiring

### Reflection 







## The hanger 

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection# CPyProjectTemplate
Put a description for your project here!
This repo is a template VS code project for CircuitPython projects that automatically uploads your code to the board when you press F5. Requires F5Anything extension.
## What does this do?
This makes it easirt to develop for boards like 
## Use


### Assignment Description
this is the swing arm it really dont do nothing but ig it's cool 

to get back in to onshape wit harder thinngs ande ready for the onshape thing.
### Evidence
![1 pic](https://github.com/korinebrown91/eg3/assets/75768362/1f37bbf9-41fa-4ba5-b7e7-c4f96cedc32b)
![unnamed (1)](https![unnamed (4)](https://github.com/korinebrown91/eg3/assets/75768362/e5cc9700-8c29-455e-8183-ff35791706d2)
://github.com/korinebrown91/eg3/assets/75768362/1bb20560-03c6-4e72-956c-0cc90c588265)


Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 
https://cvilleschools.onshape.com/documents/89d1a39801ea9e2a9c163e87/w/7655c9dc461e65180c62143c/e/91c761b8fbac0f802e60a849?renderMode=0&uiState=65381c14a787290418744324

### Reflection
i got the mass wrong so many times but everything went well im a onshape person so everthing was really easy but when i seen all the numbers i we really confused. 


&nbsp
Swing arm 
![unnamed](https://github.com/korinebrown91/eg3/assets/75768362/25cc9e87-e2dd-4480-9a2f-3398aa8c1aa5)
![![unnamed (2)](https://github.com/korinebrown91/eg3/assets/75768362/f83680bd-2d17-4c56-8d5e-40f37f3226ed)
unnamed](https://github.com/korinebrown91/eg3/assets/75768362/25cc9e87-e2dd-4480-9a2f-3398aa8c1aa5)



This is my swing arm and it is a really pretty blue. this took to long for it to get done if i followed the derections the it would have been so much better but that's fine. 

Write your assignment description here. What is the purpose of this assignment? It should be at least a few sentences.
to really get the feel of on-shape before we go into the group work and getting the hang of things 
### Evidence

Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 
https://cvilleschools.onshape.com/documents/8cc39fbb34d4ec0431a872fc/w/9659abd0cc99caa3b991344d/e/fdabb8f0d506ea5c67e69fab?renderMode=0&uiState=652edb3b7160a27eab2d5206

[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. 

### Reflection



# Multi-Part Design Studios 

 Assignment Description
![image_67146753](https://github.com/korinebrown91/eg3/assets/75768362/ced7a59d-32e0-4870-a082-d072bde9396d)
![image_67127553](https://github.com/korinebrown91/eg3/assets/75768362/cd6aa03b-845d-49bd-8f27-9f95ed74666c)


### Reflection
i feel like this a good project if your just bored and need something to do i enjoyed it but realy dint enjoy it but i do think the hardets part was the top whole of the cylce was the worst for me because i didnt really get the right demations for it but i got somewhat close. 



## Onshape_Assignment_Template
![Capture 1](https://github.com/korinebrown91/eg3/assets/75768362/e2f1d549-8c54-456f-8c96-08ac3bcfeb8d)
![Capture 2](https://github.com/korinebrown91/eg3/assets/75768362/22b75773-7885-4936-ba74-df66af286b5b)

### Assignment Description
this is my Robot Gripper idk what it does but 0

Write your assignment description here. What is the purpose of this assignment? It should be at least a few sentences.

### Evidence

Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 

[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. 

### Reflection

What went wrong / was challenging, how'd you figure it out, and what did you learn from that experience? Your goal for the reflection is to pass on knowledge that will make this assignment better or easier for the next person. Think about your audience for this one, which may be "future you" (when you realize you need some of this code in three months), me, or your college admission committee!

&nbsp;

 
## CODE_Assignment_Template

### Assignment Description
This is my IR Sensors, It's really cool.
Write your assignment description here. What is the purpose of this assignment? It should be at least a few sentences.

### Description & Code
import board 
import neopixel
import digitalio

# Set up the IR Sensor using digital pin2.
ir_sensor = digitalio.DigitalInOut(board.D2)

# Set the photointerupter as an input.
ir_sensor.direction = digitalio.Direction.INPUT

# use the internal pull-up resistor.
ir_sensor.pull = digitalio.Pull.UP

#while loop runs the inside continuously.

whilr True:

   # if an object is near the IR sensor (sensor is LOW):
       #Print something to ther Serial Monitor.
 

 #if nothing is near the IR sensor (sensor is HIGH):
   #Print something to the Serial Monitor. 

   #Intialize the on-board neopixel and set the brightness.
led = neopixel.NeoPixel(board.NEOPIXEL, 1 )
Led.brightness = 0.3

   #While loop runs the code inside continuously.
    
while True: 
 # if an object is near the IR sensor (sensor is LOW): 
 #print something to the Serial Monitor.

 #if nothing is near the IR sensor(sensor is HIGH):
 #Print something to the Serial Monitor. 
 # Intialize the on-board neopixel and set the brightness.
 led = neopixel.NeoPixel(board.NEOPIXEL, 1)
 led.brightness = 0.3
 #While loop runs the code inside continuously.
 while True: 
   #If an object is near the IR sensor (sensor is LOW):
       #Set the NeoPixel's color tp RED.

#If nothing is near the IR sensor (sensor is HIGH):
  #Set the NeoPixel's color to GREEN.  #wont let me link


Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 
![image_50441985](https://github.com/korinebrown91/eg3/assets/75768362/94b718f7-a64b-4a93-9e1b-5a06cec83e7f)


### Reflection
won't really hard just had to rush and do it. i like this coding because it wont really hard and we did something like this last year. the hardest  part was putting the wiring in the right spots other then that it was cool.
