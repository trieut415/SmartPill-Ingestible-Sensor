# SmartPill Ingestible Sensor

## Date
September 20, 2024

---

## Overview

The SmartPill project involves the design and implementation of an "ingestible" device capable of capturing, logging, and transmitting biometric data as it passes through the human body. This proof-of-concept focuses on collecting sensor data periodically, converting it into engineering units, and displaying the results on a console interface. Currently this is a rough implementation on a breadboard using the ESP32, within the ESP-IDF framework.

### Key Functionalities

1. **Temperature Measurement**
   - Reads and reports temperature in °C or °F.

2. **Light Measurement**
   - Measures light intensity in Lux using a light sensor.

3. **Battery Voltage**
   - Reads and reports battery levels via a voltage divider circuit.

4. **Tilt Orientation**
   - Detects tilt status and reports it as a logical value (on/off) to indicate device orientation.

5. **LED Status Indicators**
   - **Green LED**: Indicates "ready-to-swallow" mode (light sensor detects light).
   - **Blue LED**: Indicates sensing mode (light sensor detects darkness). Blinks every 2 seconds.
   - **Red LED**: Indicates sensing is complete (light sensor detects light again, signifying device exit).

6. **Data Reporting**
   - Reports sensor data every 2 seconds, including:
     - Temperature
     - Light levels in Lux
     - Battery voltage
     - Tilt orientation

---

## Implementation

### System Design

#### Startup Sequence
- **Initialization**: Device powers on in "ready-to-swallow" mode, activated via button press or power reset.
- **Sensing Cycle**: The system operates in a 2-second loop to capture and report data.

#### State Machine Workflow
The device transitions between three states based on sensor readings:

1. **STATE_READY**:
   - **Green LED** is active.
   - Transition to sensing mode when light intensity drops below a defined threshold.

2. **STATE_SENSING**:
   - **Blue LED** blinks every 2 seconds.
   - Sensor data is captured and logged to the console.
   - Transition to the "done" state when light intensity rises above the threshold.

3. **STATE_DONE**:
   - **Red LED** activates.
   - Sensing stops, indicating the device has exited the body.

### Task Breakdown

#### Sensor Task
Handles all sensor readings and LED state management:
- Reads:
  - **Temperature**: Captured via a thermistor.
  - **Battery Voltage**: Monitored via ADC channels.
  - **Light Intensity**: Measured and converted into Lux.
- State transitions:
  - **Ready Mode → Sensing Mode → Done Mode**
- Logs data to the console every 2 seconds.

#### Tilt Button Task
- Monitors the tilt sensor.
- Updates tilt orientation (Vertical/Horizontal) based on button press.

#### Reset Button Task
- Monitors the reset button.
- Resets the system to the "ready-to-swallow" state upon button press.

---

## Results and Challenges

### Results
The SmartPill successfully demonstrated the following:
- Accurate temperature, light intensity, battery voltage, and tilt orientation readings.
- LED indicators transitioned correctly between states based on sensor data.
- Sensor data was logged to the console in engineering units every 2 seconds.

### Challenges
1. **Tilt Sensor Integration**: The lack of proper sensors complicated tilt detection.
2. **Light Sensor Calibration**: Fine-tuning light thresholds for state transitions required extensive adjustments to account for varying lighting conditions.

### Improvements
- Replace polling mechanisms for the reset button with a hardware interrupt to optimize CPU usage.
- Simplify the circuit by minimizing the use of jumper cables.

---

## Demonstrations

- [Device Functionality Demo](https://drive.google.com/file/d/1CU57YWfw8BjZGP4tDwL273PEkrWFR-8J/view?usp=sharing)
- [Design Walkthrough](https://drive.google.com/file/d/11GS_PD7nRqs_4I9aimhMB19hdrCAkj27/view?usp=sharing)

---

## Future Enhancements
- **Hardware Refinement**: Improve sensor integration and circuit design.
- **Software Optimization**: Implement more efficient algorithms and reduce power consumption.
- **Miniaturization**: Explore opportunities to make the device smaller for practical use.

---

## Conclusion

The SmartPill project successfully demonstrated the feasibility of an ingestible sensor capable of capturing and transmitting biometric data. With further refinement, this concept could serve as a foundation for advanced medical diagnostics or health monitoring tools.
