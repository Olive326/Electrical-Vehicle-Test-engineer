# Electro-mechanical Latch Control Logic

This document presents an abstracted control architecture derived from prior industry experience. All proprietary details have been omitted.

## 1 System overview:
A bi-directional motor-driven latch mechanism with:
- Position feedback switches
- Mechanical state validation
- Diagnostic connector interface
- Motor direction control

## 2 Functional Architecture
- Mechanical Layer: mechanical transitions (open-secondary-primary)
- Sensor Layer: switch feedback validation
- Control Logic Layer: motor forward/reverse control

## 3 State machine design
![state-machine-design](https://github.com/user-attachments/assets/2f742f45-4ad2-4ac1-be5a-001e35fc286d)


## 4 Diagnostic Interface Design
A multiple-pin diagnostic connector was used to expose key sensor signals for debugging and production validation.

** Sensor Pin ** (all belong to mechanical switch not encoder): 
- Home: indicates whether the latch mechanism has returned to the neutral location
- Pawl：indicates whether the pawl is fully engaged in the primary lock position
- Ajar：indicates whether the door is full closed or open

** Common **：
- Common ground shared by all switch signals 

** Motor pin **:
- Provide bidirectional motor drive(forward/backward)
