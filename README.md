# MOSFET Brake-Light Backup Circuit

A hardware-only backup that turns on a 12V brake light when a 0–5V
pressure sensor exceeds 2.5V. No code, no microcontroller.

## Design
- BS170 N-channel MOSFET as a low-side switch
- Voltage divider R1 = 10kΩ, R2 = 52.5kΩ (k = 0.84) maps 2.5V input to the 2.1V gate threshold
- Lamp modeled as 100Ω → about 115mA when on (BS170 limit: 500mA)

## Simulation (LTspice)
- 0–5V ramp input, transient analysis
- Current starts rising at Vin ≈ 2.50V (`.meas`)
- Limitation: the turn-on is gradual, not sharp. A comparator with hysteresis would give a clean switch.

## Files
- `brake_light_backup.asc` – LTspice schematic
- Report (PDF, Hebrew)
