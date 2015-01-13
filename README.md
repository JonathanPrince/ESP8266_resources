# ESP8266_resources
General Resources for ESP8266

##Simple Serial repeater with Arduino

For writing AT commands to ESP8266 using an Arduino as a USB-UART adaptor.

Connect ESP8266 to Arduino using pins 10 and 11 as RX and TX respectively, 3.3v and GND. 
(A diagram for an ESP8266 breakout board will be coming soon)

Upload following code to the Arduino.

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

Open Arduino Serial Monitor. Tools->Serial Monitor

Set Arduino Serial Monitor to 9600 baud, line ending to "Both NL & CR".

Reset ESP8266 and you should see something like the following in the serial monitor:

```
ó£àåP%ÐÇCÁaæ l!ÈÍ$#vÿFgØ¡P¥øùæ |gø
[Vendor:www.ai-thinker.com Version:0.9.2.4]

ready
```

The second test would be to try an AT command such as `AT+GMR` which should respond with
the firmware version of your ESP8266 module.

**Connecting to an access point**
```
AT+CWJAP="<access point ssid>","<key>"
```

**Check IP address**
```
AT+CIFSR
```
