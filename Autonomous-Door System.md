# Autonomous Door System 
The autonomous Door system controls automatic opening and closing of vehicle doors.
The systems receives external triggers and executes motion based on current door state.

## Main Components:
- 12V Brush motors
- STM32F103
- L298N / TB6612 Motor driver
- Hall sensor(inside motor)
- RC circuit
- Current detection circuit

## Software Structure
**Main Control Loop**
The main() function continously performs:
1. Inpute detection:
   - Physical button
   - Bluetooth signal
   - NFC signal
2. Door state detection
   - Closed
   - Opened
   - Opening
   - Closing
3. Execute control logic based on:
   - Current state
   - External trigger
4. Protection monitoring
   - Anti-pinch
   - Anti-collision
   - Anti-tamper

![406ddf94ec4b78676ad8a3b4578643e3](https://github.com/user-attachments/assets/871e6254-2fb3-4aa7-9aa7-bd04a060f9dc)

## Important Function

**Smooth Closing Process**
Smooth closing is achieved by multi-stage speed control.

First, a self-learning process records:
- Hall sensor range for fully open
- Hall sensor range for fully closed
  
Then the motion is divided into 3 phases:
1. Initial acceleration phase
2. Constant speed phase
3. Slow down phase
Each phase uses different PWM speed settings.
This ensures smooth and stable door movement.

**Anti-pinch and Anti-collision**
Both Hall-sensor and motor current are used.
**Step 1 -Learn Normal Values**
The system records:
- Normal current range
- Normal hall pulse range
  
**Step 2 -Real-Time Monitoring**
The system records:
- Normal current range
- Normal hall pulse range 
Once both the
- hall pulse count and
- current exceeds the threshold
Then
- Trigger anti-pintch(if closing)
- Trigger anti-collision(if opening)
- Reverse motor immediately

**Anti-amper**
To prevent abuse:
- Count button press times
- if press count > 10 times
- Within limited time window
Then:
- System enters forzen mode
- No reponse for 1-2 minutes.
This protects motor and driver from overheating.
