## Hardware Connections

Connect the HC-05 to Arduino:

| HC-05 pin | Arduino connection |
|---|---|
| VCC | 5V |
| GND | GND |
| TX | RX (pin 0) |
| RX | TX (pin 1) |
| EN/KEY | Leave unconnected (unless configuring AT commands) |

## Arduino Side Code

```cpp
void setup() {
    Serial.begin(9600); // HC-05 default baud
}

void loop() {
    Serial.println("Hello Pi");
    delay(1000);

    // If Pi sends data back
    if (Serial.available()) {
        char c = Serial.read();

        // Echo received char back
        Serial.print("Got from Pi: ");
        Serial.println(c);
    }
}
```

## Raspberry Pi Side

### 1. Install the required packages

Run the following command in the terminal:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y bluetooth bluez bluez-tools rfcomm python3-serial
```

### 2. Turn on Bluetooth

Start the Bluetooth command-line utility:

```bash
bluetoothctl
```

### 3. Scan for the HC-05 module

Run these commands inside `bluetoothctl`:

```text
power on
agent on
scan on
```

Note down the MAC address of the HC-05 module (for example, `00:18:E4:35:9D:8B`).

### 4. Pair and connect

Replace the placeholder address with the HC-05 MAC address:

```text
pair XX:XX:XX:XX:XX:XX
trust XX:XX:XX:XX:XX:XX
connect XX:XX:XX:XX:XX:XX
```

### 5. Bind the Bluetooth device to an RFCOMM device

Exit `bluetoothctl`:

```text
scan off
quit
```

Then run:

```bash
ls /dev/rfcomm*
sudo rfcomm release 0
sudo rfcomm bind 0 XX:XX:XX:XX:XX:XX
ls -l /dev/rfcomm0
```

Replace `XX:XX:XX:XX:XX:XX` with the actual HC-05 MAC address.

### 6. Run the Python application

```bash
python3 bt_connect.py
```

## Raspberry Pi Python Application

Create a Python file named `bt_connect.py`:

```python
import serial
import time

# Connect to HC-05 serial port
bt = serial.Serial("/dev/rfcomm0", baudrate=9600, timeout=1)

while True:
    # Read data from Arduino
    data = bt.readline().decode('utf-8').strip()
    if data:
        print("From Arduino:", data)

    # Send message to Arduino
    bt.write(b'H')
    time.sleep(2)
```
