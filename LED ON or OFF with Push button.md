## LED ON/OFF
```python
from gpiozero import LED
from time import sleep
led = LED(18)
while True:
    led.on()
    print("LED ON")
    sleep(1)
    led.off()
    print("LED OFF")
    sleep(1)
```

## LED ON/OFF with Push Button
```python
from gpiozero import LED, Button
from time import sleep
led = LED(18)
button = Button(17)
while True:
    if button.is_pressed:
        led.on()
        print("LED ON")
        sleep(1)
    else:
        led.off()
        print("LED OFF")
        sleep(1)
```
