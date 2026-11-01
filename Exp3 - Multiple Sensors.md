## LED & Motion Sensor
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

## LM35 Sensor (Arduino)
| MCP3008 pin | Raspberry Pi physical pin | 
|-------------|---------------------------|
| 16 VDD	Pin 1 | 3.3V |
| 15 VREF	| 3.3V |
| 14 AGND |	 GND |
| 13	DGND |	  GND |
| 12	CLK	|   GPIO11 |
| 11	DOUT |	  GPIO9 |
| 10	DIN	|   GPIO10 |
| 9	CS	|   GPIO8 |
| 1	CH0	| LM35 - Vout |

```python
from gpiozero import MCP3008
from time import sleep

sensor = MCP3008(channel=0, max_voltage=3.3)

while True:
    voltage = sensor.value * 3.3
    temperature = voltage * 100
    print("Temperature:", round(temperature, 1), "°C")
    sleep(1) 
```

## IR Sensor (Arduino)
```python
from gpiozero import DigitalInputDevice
from me import sleep

ir = DigitalInputDevice(23, pull_up=False)

while True:
    if not ir.value:
        print("Object Detected!")
    else:
         print("No Object Detected.")
    sleep(0.5) 

```
