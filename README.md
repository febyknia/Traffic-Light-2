>👩🏻‍💻Feby 🗓 4 March 2025

# ESP32 BASED TRAFFIC LIGHT SIMULATION 2
---
## **A. Introduction**

This project is a traffic light simulation activity using Wokwi based on ESP32 Microcontroller and Visual Studio Code C++ programming language. The output of this simulation is button 1 pressed, red light blinks 5 times, button 2 pressed, red and green lights blink alternately, button 3 pressed, red, yellow, and green lights blink alternately.

## **B. Diagram**
This diagram was created using the ESP32 Microcontroller based Wokwi simulation.

<img width="1020" alt="1" src="https://github.com/user-attachments/assets/1db7c565-c6a1-44f8-9d91-d8533fa29b32" />



```json
{
  "version": 1,
  "author": "Anonymous maker",
  "editor": "wokwi",
  "parts": [
    { "type": "board-esp32-devkit-c-v4", "id": "esp", "top": -28.8, "left": -91.16, "attrs": {} },
    {
      "type": "wokwi-led",
      "id": "led1",
      "top": 37.2,
      "left": 141,
      "rotate": 90,
      "attrs": { "color": "red", "flip": "" }
    },
    {
      "type": "wokwi-led",
      "id": "led2",
      "top": 75.6,
      "left": 141,
      "rotate": 90,
      "attrs": { "color": "green", "flip": "" }
    },
    {
      "type": "wokwi-led",
      "id": "led3",
      "top": 56.4,
      "left": 141,
      "rotate": 90,
      "attrs": { "color": "yellow", "flip": "" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r1",
      "top": 80.75,
      "left": 48,
      "attrs": { "value": "1000" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r2",
      "top": 99.95,
      "left": 48,
      "attrs": { "value": "1000" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r3",
      "top": 61.55,
      "left": 48,
      "attrs": { "value": "1000" }
    },
    {
      "type": "wokwi-pushbutton-6mm",
      "id": "btn1",
      "top": 84.2,
      "left": -124.8,
      "attrs": { "color": "black", "xray": "1" }
    },
    {
      "type": "wokwi-pushbutton-6mm",
      "id": "btn2",
      "top": 65,
      "left": -124.8,
      "attrs": { "color": "black", "xray": "1" }
    },
    {
      "type": "wokwi-pushbutton-6mm",
      "id": "btn3",
      "top": 103.4,
      "left": -124.8,
      "attrs": { "color": "black", "xray": "1" }
    }
  ],
  "connections": [
    [ "esp:TX", "$serialMonitor:RX", "", [] ],
    [ "esp:RX", "$serialMonitor:TX", "", [] ],
    [ "esp:16", "r2:1", "black", [ "h0" ] ],
    [ "esp:5", "r1:1", "black", [ "h0" ] ],
    [ "esp:19", "r3:1", "black", [ "h0" ] ],
    [ "r3:2", "led1:A", "black", [ "v0" ] ],
    [ "r1:2", "led3:A", "black", [ "v0" ] ],
    [ "r2:2", "led2:A", "black", [ "v0" ] ],
    [ "esp:GND.3", "led1:C", "black", [ "h0" ] ],
    [ "led1:C", "led3:C", "black", [ "h-9.6", "v19.6" ] ],
    [ "led3:C", "led2:C", "black", [ "h-9.6", "v19.6" ] ],
    [ "esp:GND.1", "btn3:2.r", "black", [ "h0" ] ],
    [ "esp:33", "btn2:1.r", "black", [ "h0" ] ],
    [ "esp:26", "btn1:1.r", "black", [ "h0" ] ],
    [ "esp:14", "btn3:1.r", "black", [ "h0" ] ],
    [ "btn2:2.r", "btn1:2.r", "black", [ "h10.4", "v29.2" ] ],
    [ "btn1:2.r", "btn3:2.r", "black", [ "h10.4", "v29.2" ] ]
  ],
  "dependencies": {}
}
```

## **C. Program Code**
This program code is to set the traffic lights to turn on alternately according to a predetermined duration.

```cpp
#include <Arduino.h>

int button1 = 33;
int button2 = 26;
int button3 = 14;

int red = 19;
int yellow = 5;
int green = 16;

void kedipred(int jumlahKedip);
void kedipredgreen(int jumlahKedip);
void kedipredyellowgreen(int jumlahKedip);

void setup() {
  pinMode(red, OUTPUT);
  pinMode(yellow, OUTPUT);
  pinMode(green, OUTPUT);

  pinMode(button1, INPUT_PULLUP);
  pinMode(button2, INPUT_PULLUP);
  pinMode(button3, INPUT_PULLUP);

  Serial.begin(115200);
}

void loop() {
  if (digitalRead(button1) == LOW) {
    Serial.println("Button 1");
    kedipred(5);
  }

  else if (digitalRead(button2) == LOW) {
    kedipredgreen(5);
  }

  else if (digitalRead(button3) == LOW) {
    kedipredyellowgreen(5);
  }
}

void kedipred(int jumlahKedip) {
  for (int i = 0; i < jumlahKedip; i++) {
  digitalWrite(red, HIGH);  
  delay(500);                    
  digitalWrite(red, LOW);  
  delay(500);                   
  }
}

void kedipredgreen(int jumlahKedip) {
  for (int i = 0; i < jumlahKedip; i++) {
  digitalWrite(red, HIGH);
  digitalWrite(green, LOW);
  delay(500); 
  digitalWrite(red, LOW);
  digitalWrite(green, HIGH);
  delay(500); 
  }
}

void kedipredyellowgreen(int jumlahKedip) {
  for (int i = 0; i < jumlahKedip; i++) {
  digitalWrite(red, HIGH);
  digitalWrite(yellow, LOW);
  digitalWrite(green, LOW);
  delay(500); 
  
  digitalWrite(red, LOW);
  digitalWrite(yellow, HIGH);
  delay(500); 
  
  digitalWrite(yellow, LOW);
  digitalWrite(green, HIGH);
  delay(500); 
  
  digitalWrite(green, LOW);
  }
}
```
This simulation successfully turns on with the red light successfully flashing 5 times, the red and green lights flashing alternately, and the red, yellow, and green lights flashing alternately. Red, yellow, and green lights flash alternately. For more details, please follow the implementation steps in the traffic light report 2.
