## LED & Motion Sensor
```python
from gpiozero import LED, MotionSensor
from time import sleep
led = LED(18)
pir = MotionSensor(17)
print('Waiting for motion...')
while True:
    pir.wait_for_motion()
    print('Motion Detected!')
    led.on()
    sleep(2)
    led.off()
    print('LED OFF')

```

## LM35 Sensor (Arduino)
| MCP3008 pin | Raspberry Pi physical pin | 
|-------------|---------------------------|
| VDD | 3.3V |
| VREF | 3.3V |
| AGND |	 GND |
| DGND |	  GND |
| CLK	|   GPIO11 (SCLK) |
| DOUT |	  GPIO9 (MISO) |
| DIN	|   GPIO10 (MOSI) |
| CS	|   GPIO8 (CE0) |
| CH0	| LM35 - Vout |

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
