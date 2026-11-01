## 1)	Servo Motor:
```python
import time
from gpiozero import AngularServo

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
    servo.close()
```

## 2)	ULN2003 Stepper Motor:
```python
from gpiozero import OutputDevice
from time import sleep
# Pin Definitions
IN1 = OutputDevice(17)
IN2 = OutputDevice(18)
IN3 = OutputDevice(27)
IN4 = OutputDevice(22)
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

    sequence = step_sequence if direction > 0 else reversed(step_sequence)

    for _ in range(steps):
        for step in (sequence):
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

## 3) L298N
```python
import RPi.GPIO as GPIO
import time

# Use BCM pin numbering
GPIO.setmode(GPIO.BCM)

IN1 = 27
IN2 = 22
ENA = 18

GPIO.setup(IN1, GPIO.OUT)
GPIO.setup(IN2, GPIO.OUT)
GPIO.setup(ENA, GPIO.OUT)

# Setup PWM on ENA at 100Hz
pwm = GPIO.PWM(ENA, 100)
pwm.start(100)  # 100% speed

try:
  print("Moving Forward")
  GPIO.output(IN1, GPIO.HIGH)
  GPIO.output(IN2, GPIO.LOW)
  time.sleep(2)

  print("Stopping")
  GPIO.output(IN1, GPIO.LOW)
  GPIO.output(IN2, GPIO.LOW)
  time.sleep(1)

  print("Moving Backward")
  GPIO.output(IN1, GPIO.LOW)
  GPIO.output(IN2, GPIO.HIGH)
  time.sleep(2)

finally:
  pwm.stop()
  GPIO.cleanup()
```
