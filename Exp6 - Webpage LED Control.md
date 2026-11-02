## Steps

### Step 1: Connect Ethernet cable to Raspberry Pi as the Chit specifies (on LAN), so you should be able to open the webpage on another pc.

### Step 2: Update Raspberry Pi

Open the Raspberry Pi terminal and execute:

```bash
sudo apt update
```

### Step 3: Install the required GPIO library

```bash
sudo apt install python3-gpiozero -y
```

### Step 4: Check the Raspberry Pi IP address

Run:

```bash
hostname -I
```

Example output:

```text
10.112.55.6
```

Use the IP address assigned to your Raspberry Pi by the mobile hotspot. Your IP address may be different.

### Step 6: Run the Python program

- Click the **Run** button in Thonny.
- The web server will start listening on port `8000`.

### Step 7: Open the webpage

On another PC connected on same LAN (make sure it is set as Private Network in Network Settings), open a web browser and enter:

```text
http://<RASPBERRY_PI_IP>:8000
```

For example, if `hostname -I` displays `10.112.55.6`, open:

```text
http://10.112.55.6:8000
```

Replace the example IP address with the actual Raspberry Pi IP address.

### Step 8: Test the LED

1. Open the webpage.
2. Click the **Blink LED** button.
3. The browser sends a request to the Python server at the `/blink` endpoint.
4. The LED connected to GPIO 17 blinks five times.

### Step 9: Stop the program

In Thonny, click the **Stop** button to stop the web server.

## Hardware Connections

Connect the LED to the Raspberry Pi as follows:

| LED connection | Raspberry Pi connection |
|---|---|
| Anode (long leg) | GPIO 17 (physical pin 11) through a 220 Ω resistor |
| Cathode (short leg) | GND |

## Code

### Python Web Server — `app.py`

```python
from http.server import HTTPServer, BaseHTTPRequestHandler
from gpiozero import LED
import time

led = LED(17)


class Server(BaseHTTPRequestHandler):

    def do_GET(self):
        if self.path == "/blink":
            for i in range(5):
                led.on()
                time.sleep(0.3)
                led.off()
                time.sleep(0.3)

        html = """
        <html>
        <body>
            <h1>LED Control</h1>
            <button onclick="fetch('/blink')">Blink LED</button>
        </body>
        </html>
        """

        self.send_response(200)
        self.send_header("Content-type", "text/html")
        self.end_headers()
        self.wfile.write(html.encode())


HTTPServer(("0.0.0.0", 8000), Server).serve_forever()
```
