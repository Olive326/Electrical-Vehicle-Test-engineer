# Common probelms in Autonomous door system project

## 1. Power Supply & Noise Issues
**Problem**: Car 12V power is very noisy with voltage spikes

**Solution**: Add RC filter circuit before the DC converter to remove voltage spikes (used resistor R=___ and capacitor C=___)
Separate the MCU power supply from the motor driver power supply

**Problem**: Motor back-EMF (reverse voltage)
When brushed motors suddenly stop, they create high voltage spikes that can burn the MCU:

**Solution**: Add TVS diode (Transient Voltage Suppressor) and flyback diode at the motor
Use star grounding: Connect motor ground, Hall sensor ground, and MCU ground all to DC ground separately to prevent noise interference

## 2. Signal Sampling Noise
**Problem**: Hall sensor and limit switch signals have jitter/bouncing

- Hardware solution: Twist the Hall sensor wires together to reduce electromagnetic interference (reduces common-mode noise)
- Software solution: Add debounce logic to filter out false signals

**Problem**: Anti-pinch detection false triggers

- Add current sensing module (small 50mΩ resistor + op-amp)
- Use dual detection: Hall sensor + current spike detection together for more accurate anti-pinch
- Software: Add hysteresis logic to avoid false triggers from small fluctuations

## 3. Reference Position Setup

- Measure normal operating current using getLimitCurrent() function
- Do automatic homing/calibration at startup: Run motor slowly to mechanical limits to set zero position
- Save maximum and minimum positions

## 4. Wrong Motor Driver Choice
**L298N driver problems**:

High voltage drop → motor has weak torque
Gets hot easily → triggers thermal protection → unstable

**BTS7960 driver (better choice)**:

Higher power, can handle large current
Built-in overcurrent and overheating protection

**Anti-Pinch Calibration Process**:

- Set PWM duty cycle for three speed stages (slow/medium/fast)
- Measure normal operating current for each stage
- Physically test the pinch force for each stage
- Fine-tune PWM duty cycle and current limits based on force measurements
