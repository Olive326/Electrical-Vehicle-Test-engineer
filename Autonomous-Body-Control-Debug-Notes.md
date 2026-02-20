## Basic Debug Logic
Before starting any troubleshooting, I always make sure the following information is clear:

**1.State-Sensor Logic table**
This defines:
- Which sensor lead to which system sction
- The judgement rules inside MCU
- Protection conditions and trigger conditions
Without this table, it's impossible to know whether the system behavior is correct or not

**2.Control Timing Disgram**
- Signal sequence
- Delay between signals
- Action flow of actuators
  
**3.Connector Pin Definition**
Pin definition is necessary for:
- Debug wiring
- Signal measurement
  
**4.Reproduce the issue**
I always try to reproduce the issue at the failure scene:
- Same car
- Same power condition
- Same motor

### System Architecture Overview
The elctrical systems I mainly worked on include:
- Window control system
- Back-door control system
- Power tailgate
- Wiper system
  
Although the functions are different, their control architecture is very similar:

**General Architecture**
- One MCU controls the actuators(motor driver side)
- Another MCU is linked with latch motor
- A confirmation signal is sent between modules
- Some signals are hardwired to avoid CAn delay(like window wiper)

### Common Debug Framework

**Step 1 - Power Intergrity**
- 12V supply stable
- DC/DC output normal
  
**Step 2 - Signal Validity**
- Signal voltage lavel correct ?
- Signal duration meets requirements?
- Signal qualified by MCU?
  
**Step 3 - Control Logic**
- Is state machine correct?
- Is protection triggered?
- Is calibration lost?

**Step 4 - Control Logic**
- Any interference?
- Any misalignment?
- Any extra resistance(like low tempereture)?

**Step 5 - Communication**
- CAN/LIN offline?
- Message timeout?

### Case Studies
**Case 1 – Only Left Front Window Works**
**Symptom**
- Only left front window can be controlled.
- Other window switches are invalid.

**Investigation**
- Window switch click is normal
- Logic input detected
- Harness checked

**Root Cause**
Window control harness issue.

**Case 2 – Power tailgate Motor Burned**
**Symptom**
- Motor damaged due to overheating.

**Investigation**
- Position switch kept being triggered as long as car moved.
- Motor continuously stalled.

**Root Cause**
Harness issue caused false triggering of position switch signal.

**Case 3 – Window Cannot Reach Top**
**Possible Causes**
- Self-learning calibration error
- Quater glass structural issue

**Case 4 – Back Door Cannot Fully Lock**
**Symptom**
- After full lock, it rebounce to half-lock position

**Root Cause**
- Guide block misalignment
- Striker adjustment incorrect
- Harness attached on sealing surface
Mechanical interference prevents full closure

**Case 5 – Four Doors Windows Abnormal Noise**
**Root Causes**
- Inner and outer belt weatherstrip interference
- Mechanical friction caused abnormal sound

**Wiper System Case**
**Case 6 – Wiper Stalling**

**Symptom**
- Wiper intermittently stalls

**Root Cause**
- Reset signal not properly release or recognized as valid
- Reset pulse failed qualification window:

**Mechanism**
- Duration less than x ms
- Voltage lower than x V threshold

**Low Temperature Aggravation**
At low temperature:
- Relay actuation slows
- Inrush current increase
- Driver IC protection triggered

**Case 7 – Vehicle Sudden Power Off**
**Scenario A- Voltage Drops to 0v**
- Power distribution path issue
- 12V bus separated from main power distribution module

**Scenario A- Voltage Not 0v**
- DC/DC overcurrent protection
- Load surge
- Low temperature reduces motor resistence
  
**Case 8 – Brake Pedal Vibration**
In new energt vehicle:
- Light press: regenerative vraking
- Deep press: hydraulic brake blended

**Possible Causes**
- Regenerative and hydraulic blending abnormal
- Wheel speed sensor signal error - false ABS trigger
- Low voltage supply unstable

**Case 9 – EPS Extra 1/4 Turn**
**Possible Causes**
- EPS end-stop learning lost after vehicle power drop
- Steering angle sensor abnormal

**Case 10 – Back Door External Switch Invalid but UI shows Open**
**Possible Causes**
Communication issue:
- CAN\LIN offline
- Command not executed
Execution module issue:
- Protection mode
- Overcurrent/ndervoltage/overtemp



