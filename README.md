# CircuitPython
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
Make an account with your Google ID at [tinkercad.com](https://www.tinkercad.com/learn/circuits), and use "TinkerCad Circuits to make a wiring diagram."  It's really easy!  
Then post an image here.   [here's a quick tutorial for all markdown code, like making links](https://guides.github.com/features/mastering-markdown/)

### Reflection 
what went wrong was the wiring it kinda got me off graud a liittle with all wirse. Overall ever thng was good and i got the moter to move i learn that i dont have to put 5v and grd when im using my better pack. i reallylike this one because the code wont long and the wiring was hard but i got on to it quick.



## Hello_CircuitPython

### Description & Code
Description goes here

Here's how you make code look like code:

```python
Code goes here

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
### Wiring

![WiringSolution](images/I2C_M4_Solution.png)






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







## NextAssignment

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
### Every new project:
1. Make a GitHub account if you don't have one with your normal school credentials and sign into it.
2. Click the big green Use This Template button at the top of this page.
3. Name the new repository something appropriate to the purpose of your project (Your first one should probably be named `Engr3`).
4. Hit "Create repository from template." (The default settings should be fine.)
5. Open VS Code on your machine. Click Clone Repository. If it doesn't show up, hit Ctrl+Shift+P and then type Clone, then hit Enter.
6. Paste in the link to the new repository you've just created from the template and hit enter.
7. For the location, Documents folder.
8. Hit "Open Cloned Directory" in the bottom-left corner.
9. Install the reccomended extensions when you get that popup in the lower right corner. IF the pop-up dissapears before you can click it, hit the tiny bell icon in the lower left corner to bring it back.
### To commit from VS Code:
1. Go to the little branch icon in the left bar of VS Code.
2. Click the + icon next to the files you want to commit.
3. Write a message that descibes your changes in the "Message" box and hit commit.
4. If you get an error about user.name and user.email, see the next section.
5. Click the "Sync changes" button.
### If you get an error about user.name and user.email
1. In VS Code, hit `` Ctrl+Shift+` ``
2. Filling in your actual information, run the following commands one line at a time. The paste shortcut is `Ctrl+V` or you can right click then hit paste. Spelling must match exactly:
```
git config --global user.name YOURGITHUBUSERNAME
git config --global user.email YOURSCHOOLEMAIL
```
3. Return to the previous section.
### To install a library:
1. Get the library files from the Adafruit bundle (probably a .mpy file or a folder.)
2. Copy them to the lib folder *in your project's folder, usually in Documents.* **Don't copy to the lib folder on the board! It will not work!**
3. Hit F5 and the library will be uplaoded to the board.
4. \## Onshape_Assignment_Template

### Assignment Description
this is the swing arm it really dont do nothing but ig it's cool 

to get back in to onshape wit harder thinngs ande ready for the onshape thing.
### Evidence

Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 

[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. 
![1 pic](https://github.com/korinebrown91/eg3/assets/75768362/1f37bbf9-41fa-4ba5-b7e7-c4f96cedc32b)

### Reflection
i got the mass wrong so many times but everything went well im a onshape person so everthing was really easy but when i seen all the numbers i we really confused. 
What went wrong / was challenging, how'd you figure it out, and what did you learn from that experience? Your goal for the reflection is to pass on knowledge that will make this assignment better or easier for the next person. Think about your audience for this one, which may be "future you" (when you realize you need some of this code in three months), me, or your college admission committee!

&nbsp
Swing arm 
![unnamed](https://github.com/korinebrown91/eg3/assets/75768362/25cc9e87-e2dd-4480-9a2f-3398aa8c1aa5)
![![unnamed (2)](https://github.com/korinebrown91/eg3/assets/75768362/f83680bd-2d17-4c56-8d5e-40f37f3226ed)
unnamed](https://github.com/korinebrown91/eg3/assets/75768362/25cc9e87-e2dd-4480-9a2f-3398aa8c1aa5)
![unnamed (3)](https://github.com/korinebrown91/eg3/assets/75768362/e58c9966-756d-42ae-bd10-eac42ab2c28b)

### Assignment Description

Write your assignment description here. What is the purpose of this assignment? It should be at least a few sentences.
to really get the feel of on-shape before we go into the group work and getting the hang of things 
### Evidence

Take several cropped screenshots of your Onshape document from different angles. Try to capture all important aspects of the design. Turn off overlays that obscure the parts, such as planes or mate connectors. Your images should have captions, so the reader knows what they are looking at!  

### Part Link 
https://cvilleschools.onshape.com/documents/8cc39fbb34d4ec0431a872fc/w/9659abd0cc99caa3b991344d/e/fdabb8f0d506ea5c67e69fab?renderMode=0&uiState=652edb3b7160a27eab2d5206

[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. 

### Reflection
i feel like it was good but the dementiones on the Swing Arm,it wwas really challaging but some how i got it done but it's not all the way perfect but it is 90%. there where so many things that went wrong on this assingmeant but the numbers was a bit much because it was hard to get it right but ik if i do it agian i would put the middle part in first. 
&nbsp;
