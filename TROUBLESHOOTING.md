# TROUBLESHOOTING GUIDE

## PROBLEM 1: No Output Signal (V_PEAK = 0V or Flat)

### Possible Causes & Solutions:

**1. Power supply not connected**
```
Check: Is +5V connected to Pin 8 of both U1 and U2?
Check: Is GND connected to Pin 4 of both U1 and U2?
Fix: Verify all power connections with multimeter
```

**2. Diode D1 is reversed**
```
Check: Is the LONG leg (anode) connected to U2 output?
Check: Is the SHORT leg (cathode) connected to feedback?
Fix: Flip the diode if reversed
```

**3. Capacitor C1 is not connected or dead**
```
Check: Is C1 positive connected to V_PEAK junction?
Check: Is C1 negative connected to GND?
Fix: Replace capacitor, verify polarity
```

**4. Broken wire or poor breadboard connection**
```
Check: Trace every connection with your finger
Check: Look for loose wires or bent pins
Fix: Reseat all components and wires firmly
```

---

## PROBLEM 2: Output is Following Input Signal (No Peak Holding)

### Possible Causes & Solutions:

**1. Diode D1 is not conducting**
```
Check: Is D1 anode connected to U2 output (Pin 7)?
Check: Is D1 cathode connected to U2 inverting input (Pin 6)?
Fix: Verify diode orientation and connections
```

**2. Resistor R3 is not present or disconnected**
```
Check: Is R3 (1MΩ) connected between V_PEAK and GND?
Check: Is there a path for discharge?
Fix: Add R3 if missing, or reconnect if loose
```

**3. Capacitor C1 is shorted or dead**
```
Check: Measure capacitor with multimeter (should show charge/discharge)
Check: Look for visual damage or bulging
Fix: Replace with new 10µF capacitor
```

**4. Op-amp U2 is not working (not acting as comparator)**
```
Check: Is U2 Pin 8 at +5V?
Check: Is U2 Pin 4 at GND?
Check: Try swapping U2 with a known good LM358
Fix: Replace op-amp if damaged
```

---

## PROBLEM 3: Output Jumps Randomly or is Noisy

### Possible Causes & Solutions:

**1. Poor breadboard connections**
```
Check: Are all wires fully inserted into breadboard holes?
Check: Are there any loose connections near the junction?
Fix: Push all wires firmly into breadboard
```

**2. Function generator not grounded properly**
```
Check: Is the signal generator GND connected to circuit GND?
Check: Is there a single common GND point?
Fix: Connect signal generator ground to your circuit ground
```

**3. Oscilloscope probe grounding issue**
```
Check: Are oscilloscope probe grounds connected to circuit GND?
Check: Are you using crocodile clips or proper ground connections?
Fix: Use proper ground connections, not floating probes
```

**4. Resistor R1 or R2 is loose or missing**
```
Check: Are R1 and R2 properly connected in the biasing network?
Check: Are they making good contact?
Fix: Reconnect or reseat R1 and R2
```

---

## PROBLEM 4: Peak Value is Lower Than Expected

### Possible Causes & Solutions:

**1. Diode forward voltage drop is still visible**
```
Input: 0.5V
Output: 0.4V or 0.45V (instead of expected 0.5V)
Cause: Op-amp feedback not compensating fully
Fix: Check if diode is in the feedback loop (not after output)
```

**2. Op-amp U2 output is not reaching full voltage**
```
Check: Is U2 actually going HIGH when signal increases?
Check: Is there a load on U2 output that's pulling it down?
Fix: Remove any extra connections to U2 output
```

**3. Capacitor C1 is leaking charge too fast**
```
Check: Is there a short across C1?
Check: Is the capacitor old or damaged?
Fix: Replace with a fresh 10µF capacitor
```

---

## PROBLEM 5: Peak Decays Too Quickly (Resets in < 1 second)

### Possible Causes & Solutions:

**1. Resistor R3 is too small**
```
Check: Is R3 actually 1MΩ? (Look at color bands)
Check: Did you accidentally use 1kΩ instead?
Fix: Replace with correct 1MΩ resistor
```

**2. There's an accidental path to ground**
```
Check: Is there a stray wire between V_PEAK and GND?
Check: Is there a resistor you didn't intend to add?
Fix: Remove any accidental connections
```

**3. Op-amp U2 output is leaking current**
```
Check: Is there a path for current from U2 output to ground besides R3?
Fix: Verify only R3 connects to GND from V_PEAK
```

---

## PROBLEM 6: Peak Doesn't Reset (Stays at Same Level)

### Possible Causes & Solutions:

**1. Resistor R3 is too large or missing**
```
Check: Is R3 present? Did you forget to add it?
Check: Is it actually 1MΩ or did you use 10MΩ?
Fix: Add or replace R3 with correct 1MΩ resistor
```

**2. Capacitor C1 is not discharging**
```
Check: Is there a complete circuit from C1 through R3 to GND?
Check: Are both ends of R3 properly connected?
Fix: Reconnect R3 to ensure complete discharge path
```

---

## PROBLEM 7: Oscilloscope Shows Nothing or Distorted Display

### Possible Causes & Solutions:

**1. Oscilloscope settings are wrong**
```
Check: Is the oscilloscope set to DC mode (not AC)?
Check: Is the time scale too fast (try 0.5s/div)?
Check: Is the voltage scale appropriate (try 100mV/div)?
Fix: Adjust scope settings for slow biomedical signals
```

**2. Oscilloscope probe is disconnected**
```
Check: Is the probe connected to the circuit?
Check: Is the ground clip connected to GND?
Fix: Reconnect probe and ground properly
```

**3. Input signal is not reaching the circuit**
```
Check: Does the function generator have output enabled?
Check: Is the signal generator connected to the circuit?
Check: Is the signal amplitude set correctly (50mV)?
Fix: Enable output on signal generator and verify connections
```

---

## PROBLEM 8: One Op-Amp Works, Other Doesn't

### Possible Causes & Solutions:

**1. Wrong pins connected for second op-amp**
```
Remember: LM358 has TWO op-amps
Op-Amp A: Pins 1, 2, 3 (+ power pins)
Op-Amp B: Pins 5, 6, 7 (+ power pins)

Check: Are you using correct pins for U2?
Check: Pin 5 should be U2 non-inverting input?
Check: Pin 6 should be U2 inverting input?
Check: Pin 7 should be U2 output?
Fix: Reconnect U2 to correct pins
```

**2. Second op-amp (U2) has no power**
```
Check: Pins 4 and 8 on the IC provide power to BOTH op-amps
Check: Is GND actually at Pin 4?
Check: Is +5V actually at Pin 8?
Fix: Verify power connections
```

---

## QUICK CHECKLIST BEFORE TESTING

```
☐ Power supply (+5V and GND) connected to breadboard
☐ U1 Pin 4 → GND, U1 Pin 8 → +5V
☐ U2 Pin 4 → GND, U2 Pin 8 → +5V
☐ R1 (100k) connected from signal input to U1 Pin 3
☐ R2 (100k) connected from U1 Pin 3 to GND
☐ U1 Pin 1 connected to U1 Pin 2 (feedback)
☐ U1 Pin 1 connected to U2 Pin 5 (signal path)
☐ U2 Pin 7 (output) connected to D1 anode (long leg)
☐ D1 cathode (short leg) connected to U2 Pin 6 AND V_PEAK junction
☐ C1 (10µF) positive at V_PEAK, negative at GND
☐ R3 (1MΩ) connected from V_PEAK to GND
☐ Oscilloscope CH1 on signal input (DC mode)
☐ Oscilloscope CH2 on V_PEAK output (DC mode)
☐ Function generator GND connected to circuit GND
```

---

## IF NOTHING WORKS

1. **Start simple:** Check power supply first (multimeter on +5V and GND)
2. **Test one op-amp at a time:** Remove U2, test U1 as buffer alone
3. **Use multimeter:** Measure voltages at key points (should be near 2.5V offset)
4. **Replace components one by one:** Start with op-amps, then diode, then capacitor
5. **Redraw the circuit:** Make sure your breadboard matches the schematic exactly

---

**Good luck! You've got this! 💪**
