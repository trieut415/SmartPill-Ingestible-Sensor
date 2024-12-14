# SmartPill Ingestible Sensor

## Date
September 20, 2024

---

## Overview

The **SmartPill** project demonstrates the design and implementation of an ingestible sensor device capable of capturing, logging, and transmitting biometric data as it passes through the digestive tract. Built on the ESP32 microcontroller within the ESP-IDF framework, this prototype focuses on real-time data collection, conversion to engineering units, and display on a console interface. 

This proof-of-concept lays the groundwork for innovative medical diagnostic tools by simulating the functionality of a disposable, ingestible sensor.

---

## Key Features

1. **Temperature Monitoring**
   - Measures and reports temperature in °C or °F.

2. **Light Intensity Measurement**
   - Reports light levels in Lux using a calibrated light sensor.

3. **Battery Voltage Monitoring**
   - Reads and reports battery voltage using a voltage divider circuit.

4. **Tilt Orientation Detection**
   - Reports tilt as a logical state (on/off) to indicate device orientation.

5. **LED Status Indicators**
   - **Green LED**: "Ready-to-swallow" mode (light sensor detects ambient light).
   - **Blue LED**: Sensing mode (light sensor detects darkness); blinks every 2 seconds.
   - **Red LED**: Sensing complete (light sensor detects ambient light again).

6. **Periodic Data Reporting**
   - Reports sensor data every 2 seconds, including:
     - Temperature
     - Light levels in Lux
     - Battery voltage
     - Tilt orientation

---

## Implementation

### System Design

#### Startup Sequence
- Device powers on in "ready-to-swallow" mode via a button press or power reset.
- A state machine governs transitions between sensing phases based on real-time sensor data.

#### State Machine Workflow
The system operates within three primary states:

1. **Ready Mode**:
   - Green LED illuminates.
   - Transition to "Sensing Mode" when light levels drop below a threshold.

2. **Sensing Mode**:
   - Blue LED blinks every 2 seconds.
   - Sensors record data, which is logged to the console.
   - Transition to "Done Mode" when light levels rise above the threshold.

3. **Done Mode**:
   - Red LED activates, signaling sensing is complete.
   - System halts data collection.

---

### Tasks and Functions

#### Sensor Task
- Reads sensor inputs:
  - **Temperature**: Captured via a thermistor.
  - **Battery Voltage**: Measured through ADC channels.
  - **Light Intensity**: Converted to Lux.
- Manages state transitions and logs data every 2 seconds.

#### Button and Interrupt Task
- **Tilt Detection**: Updates tilt orientation based on sensor input.
- **Reset Functionality**: Resets the device to "Ready Mode" upon button press.

#### LED Management Task
- Controls LED indicators to reflect the device's current state.

---

## Results and Learnings

### Achievements
- Successfully implemented real-time temperature, light, battery voltage, and tilt data acquisition.
- Achieved accurate reporting in engineering units on the serial console.
- LED indicators performed seamlessly to reflect state transitions.

### Challenges
1. **Tilt Sensor Calibration**:
   - Ensuring accurate tilt detection required adjustments due to sensor limitations.
2. **Light Threshold Tuning**:
   - Extensive testing was needed to accommodate diverse lighting conditions.

### Improvements
- Replace polling mechanisms with hardware interrupts for more efficient button handling.
- Enhance circuit design to reduce complexity and improve reliability.

---

## Demonstrations

- [Device Functionality Demo](https://drive.google.com/file/d/1CU57YWfw8BjZGP4tDwL273PEkrWFR-8J/view?usp=sharing)
- [Design Walkthrough](https://drive.google.com/file/d/11GS_PD7nRqs_4I9aimhMB19hdrCAkj27/view?usp=sharing)

---

## Future Enhancements

1. **Hardware Improvements**:
   - Integrate advanced sensors for greater accuracy.
   - Miniaturize the device for real-world application.

2. **Software Optimization**:
   - Reduce power consumption with more efficient algorithms.
   - Add wireless data transmission capabilities.

3. **Sustainability**:
   - Explore reusable or biodegradable materials for construction.

---

## Conclusion

The **SmartPill Ingestible Sensor** prototype showcases the potential of ingestible technology in medical diagnostics. While this implementation is a proof-of-concept, further refinement in hardware, software, and sustainability can elevate this design into a viable, cutting-edge medical tool.

