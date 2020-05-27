# SIT210_Task7.3D_RPiPWM-
Code for PWM Task

```
from gpiozero import LED
import RPi.GPIO as GPIO
import time as time

GPIO.setmode(GPIO.BCM)

# LED on the board
led = 26

# Ultrasonic Sensor
TRIG = 23
ECHO = 24

# Setup
GPIO.setup( led, GPIO.OUT)
GPIO.setup( TRIG, GPIO.OUT)
GPIO.setup( ECHO, GPIO.IN)


# PWM Led
pwm_led = GPIO.PWM( led, 50)
pwm_led.start(0)

def Distance():
    GPIO.output(TRIG, False)
    print "Calculating..."
    time.sleep(2)
    
    GPIO.output(TRIG, True)
    time.sleep(0.0001)
    GPIO.output(TRIG, False)
    
    while GPIO.input(ECHO)==0:
        time_start = time.time()
    
    while GPIO.input(ECHO)==1:
        time_stop = time.time()
        
    time_duration = time_stop - time_start 
    distance = time_duration * 17150
    distance = round(distance, 2)
    
    return distance
    
    
while True:

    input = Distance()
    
    if ( (input > 0 ) and (input <= 4)):
        pwm_led.ChangeDutyCycle(100)
 
    elif ( (input > 4) and (input <= 8)):   
        pwm_led.ChangeDutyCycle(75)
        
    elif ( (input > 8) and (input <= 12)):
        pwm_led.ChangeDutyCycle(50)
    
    elif ( (input > 12) and (input <= 16)):
        pwm_led.ChangeDutyCycle(25)
    
    else:
        pwm_led.ChangeDutyCycle(0)
 ```     
