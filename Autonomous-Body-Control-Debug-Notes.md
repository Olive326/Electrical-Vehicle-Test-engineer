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


