## 1)	Servo Motor:
```python
import time
from gpiozero import AngularServo
from gpiozero.pins.pigpio import PiGPIOFactory

# Initialize the servo on GPIO 18
servo = AngularServo(
    18, 
    min_angle=-90, 
    max_angle=90, 
    min_pulse_width=0.0005, 
    max_pulse_width=0.0025
)

try:
    print("Starting servo sweep. Press Ctrl+C to stop.")
    while True:
        print("Moving to -90 degrees")
        servo.angle = -90
        time.sleep(2)

        print("Moving to 0 degrees")
        servo.angle = 0
        time.sleep(2)

        print("Moving to 90 degrees")
        servo.angle = 90
        time.sleep(2)

except KeyboardInterrupt:
    print("\nProgram stopped by user.")
    servo.detach()
```

## 2)	ULN2003 Stepper Motor:
```python
from gpiozero import OutputDevice
from time import sleep
# Pin Definitions
IN1 = OutputDevice(14)
IN2 = OutputDevice(15)
IN3 = OutputDevice(18)
IN4 = OutputDevice(23)
# Define step sequence for the motor
step_sequence = [
    [1, 0, 0, 0],
    [1, 1, 0, 0],
    [0, 1, 0, 0],
    [0, 1, 1, 0],
    [0, 0, 1, 0],
    [0, 0, 1, 1],
    [0, 0, 0, 1],
    [1, 0, 0, 1]
]
def set_step(w1, w2, w3, w4):
    IN1.value = w1
    IN2.value = w2
    IN3.value = w3
    IN4.value = w4

def step_motor(steps, direction=1, delay=0.01):
    for _ in range(steps):
        for step in (step_sequence if direction > 0 else reversed(step_sequence)):
            set_step(*step)
            sleep(delay)

try:
    while True:
        steps = int(input("Enter number of steps (2048 for one full revolution): "))
        direction = int(input("Enter direction (1 for forward, -1 for backward): "))
        step_motor(steps, direction)
except KeyboardInterrupt:
    print("Program stopped by user")
```
