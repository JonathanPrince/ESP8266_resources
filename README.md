# ESP8266_resources
General Resources for ESP8266

##Simple Serial repeater with Arduino

For writing AT commands to ESP8266 using an Arduino as a USB-UART adaptor.

```cpp
#include <SoftwareSerial.h>

SoftwareSerial softSerial(10, 11);

void setup() {
  
  // Open serial connection
  Serial.begin(9600);

  // set the data rate for the softSerial port
  softSerial.begin(9600);

}

void loop() {
  
  // if data is available from softSerial write it to Serial
  if (softSerial.available()) {
    Serial.write(softSerial.read());
  }
  
  // if data is available from Serial write it to softSerial
  if (Serial.available()) {
    softSerial.write(Serial.read());
  }
  
}
```
