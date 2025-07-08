# Humanoid Servo Walk – Arduino Project

This project controls **4 servo motors** connected to an Arduino Uno using Tinkercad.  
It performs a basic sweep motion for 2 seconds, then holds all servos at 90°.

## Hardware Setup
- Arduino Uno R3
- Breadboard
- 4 Servo Motors 
- Jumper wires

### Servo Pin Mapping:
| Servo         | Function      | Arduino Pin |
|---------------|---------------|-------------|
| Servo 1       | Left Hip      | 3           |
| Servo 2       | Left Knee     | 5           |
| Servo 3       | Right Hip     | 6           |
| Servo 4       | Right Knee    | 9           |

### Power:
- Servos powered from breadboard rails connected to Arduino 5V and GND.

---

## Code Behavior

1. All 4 servos sweep from 0° to 180° and back repeatedly for 2 seconds.
2. After that, all servos go to 90° and stay there.

```
#include <Servo.h>

Servo servo1, servo2, servo3, servo4;

void setup() {
  servo1.attach(3);
  servo2.attach(5);
  servo3.attach(6);
  servo4.attach(9);
}

void loop() {
  // Sweep motion for 2 seconds
  unsigned long startTime = millis();
  while (millis() - startTime < 2000) {
    for (int pos = 0; pos <= 180; pos += 5) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(15);
    }
    for (int pos = 180; pos >= 0; pos -= 5) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(15);
    }
  }

  // Hold at 90 degrees
  servo1.write(90);
  servo2.write(90);
  servo3.write(90);
  servo4.write(90);
  while (true); // Freeze loop
}
```
## Walking Motion Algorithm

This is a simple walking cycle for a humanoid robot using 4 servos (2 per leg):

- **Servo 1**: Left Hip  
- **Servo 2**: Left Knee  
- **Servo 3**: Right Hip  
- **Servo 4**: Right Knee

### Algorithm Steps:

1. **Start Walking Loop**
2. **Right Leg Forward**  
   - Servo 3 (Right Hip) → 135° (lift forward)  
   - Servo 4 (Right Knee) → 120° (bend)
3. **Right Leg Down**  
   - Servo 3 → 90°  
   - Servo 4 → 90°
4. **Shift Weight to Right Leg**
5. **Left Leg Forward**  
   - Servo 1 (Left Hip) → 135°  
   - Servo 2 (Left Knee) → 120°
6. **Left Leg Down**  
   - Servo 1 → 90°  
   - Servo 2 → 90°
7. **Repeat loop**

Each step can be controlled with short delays and smooth angle transitions to simulate natural walking.

## Simulation

This project was tested on Tinkercad Circuits, which allows Arduino simulation with servos.
