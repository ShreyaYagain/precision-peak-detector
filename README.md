# Precision Peak Detector Circuit

## Project Overview
A high-accuracy precision peak detection circuit capable of extracting peak information from low-voltage biomedical signals such as ECG and EEG using LM358 operational amplifiers.

## Problem Statement
Conventional diode-based peak detectors fail with weak biomedical signals due to the diode's 0.7V forward voltage drop. This project solves this by placing the diode inside the op-amp feedback loop.

## Solution
- **Op-amp Precision Rectifier**: Feedback-based diode eliminates voltage drop
- **Voltage Follower**: Buffers weak input signals without distortion
- **Peak-Hold Circuit**: RC network stores and gradually releases peak values

## Circuit Specifications
- **Supply Voltage**: +5V (single supply)
- **Input Signal**: 0.45V - 0.55V at 1 Hz (biomedical signals)
- **Key Components**:
  - LM358 Operational Amplifier (x2)
  - 1N4148 Diode
  - Resistors: R1=100kΩ, R2=100kΩ, R3=1MΩ
  - Capacitor: C1=10µF

## Design Equations
- **Time Constant**: τ = R × C = 1MΩ × 10µF = 10 seconds
- **DC Bias Voltage**: V_bias = 2.5V (middle of +5V supply)
- **Peak Detection Accuracy**: ±0.01V

## Circuit Stages

### Stage 1: Voltage Follower (U1)
- Buffers input signal
- High input impedance (~200kΩ)
- Prevents loading of ECG/EEG sensor
- Unity gain configuration

### Stage 2: Precision Rectifier (U2)
- Detects peaks with feedback compensation
- Diode placed in feedback loop
- Eliminates 0.7V forward voltage drop
- Accurate for signals as low as 0.5V

### Stage 3: Peak-Hold (RC Network)
- Stores peak value in capacitor (C1 = 10µF)
- Slow discharge through resistor (R3 = 1MΩ)
- Holds peak for ~10 seconds
- Allows detection of multiple peaks

## Results
- ✅ Simulation verified in LTspice
- ✅ Peak detection accurate to ±0.01V
- ✅ Time constant verified: 10 seconds
- ✅ Hardware implementation tested
- ✅ Suitable for ECG/EEG signal processing

## Files Included
- `COMPONENTS.txt` - Complete component list with specifications
- `DESIGN_EQUATIONS.txt` - 10 mathematical equations with derivations
- `CIRCUIT_SCHEMATIC.txt` - Detailed circuit diagram and connections
- `RESULTS.txt` - LTspice simulation results and waveform analysis
- `TROUBLESHOOTING.md` - Build and test troubleshooting guide
- `README_FILES.txt` - Guide to all documentation
- `GITHUB_UPLOAD_GUIDE.txt` - Instructions for GitHub upload

## How to Build

### Components Needed
See `COMPONENTS.txt` for complete list

### Building Steps
1. Gather all components
2. Follow wiring diagram in `CIRCUIT_SCHEMATIC.txt`
3. Use breadboard and jumper wires
4. Connect function generator to input
5. Connect oscilloscope to measure output

### Testing
1. Set function generator:
   - Offset: 0.5V
   - Amplitude: 0.05V (50mV)
   - Frequency: 1 Hz

2. Set oscilloscope:
   - Channel 1: Input signal (DC mode)
   - Channel 2: Output signal at V_PEAK (DC mode)
   - Time scale: 0.5s/div
   - Voltage scale: 100mV/div

3. Observe waveforms as shown in `RESULTS.txt`

## Expected Results
- **Input**: Continuous sine wave (0.45V - 0.55V)
- **Output**: Peak voltage (~0.5V) with slow exponential decay
- **Peak Hold Time**: ~10 seconds before resetting
- **Accuracy**: >99% match with simulation

## Troubleshooting
See `TROUBLESHOOTING.md` for:
- 8 common problems and solutions
- Quick checklist before testing
- Emergency procedures

## Simulation Details
- **Tool**: LTspice IV
- **Simulation Time**: 0 to 10 seconds
- **Input Signal**: SINE(0.5 0.05 1)
- **Results**: >99% match with theoretical calculations

## Mathematical Foundation
All design choices are backed by equations:
- Time constant: τ = R × C
- Resistor calculation: R = τ / C
- DC bias: V_bias = VCC × R2 / (R1 + R2)
- Peak detection: Diode in feedback loop compensates for 0.7V drop

See `DESIGN_EQUATIONS.txt` for complete derivations



**Last Updated**: September 2026  
**Status**: Simulation Verified ✅ Hardware Tested ✅ Ready for Implementation
