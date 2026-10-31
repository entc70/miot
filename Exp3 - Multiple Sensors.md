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
```cpp
const int LM35_PIN = A0;  // LM35 analog output pin

void setup() {
  Serial.begin(9600);  // Start serial communication at 9600 baud
}
void loop() {
  int lm35Value = analogRead(LM35_PIN);  // Read analog value from LM35
  float temperature = (lm35Value * 5.0 / 1023.0) * 100;  // Convert to Celsius

  // Display temperature on Serial Monitor
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  delay(1000);  // Wait for 1 second
}
```

## IR Sensor (Arduino)
```cpp
const int IR_PIN = 3;  // IR sensor output pin

void setup() {
  pinMode(IR_PIN, INPUT);  // Set IR pin as input
  Serial.begin(9600);      // Start serial communication at 9600 baud
}
void loop() {
  int irValue = digitalRead(IR_PIN);  // Read IR sensor state

  if (irValue == LOW) {  // Object detected (active LOW)
    Serial.println("Object Detected!");
  } else {
    Serial.println("No Object Detected.");
  }
  delay(500);  // Small delay for stability
}

```
