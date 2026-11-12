# MOSFET Brake-Light Backup Circuit

A hardware-only backup that turns on a 12V brake light when a 0–5V
pressure sensor exceeds 2.5V. No code, no microcontroller.

## Design
- BS170 N-channel MOSFET as a low-side switch
- Voltage divider R1 = 10kΩ, R2 = 52.5kΩ (k = 0.84) maps 2.5V input to the 2.1V gate threshold
- Lamp modeled as 100Ω → about 115mA when on (BS170 limit: 500mA)

## Simulation (LTspice)
- Input: 0–5V ramp over 1s (`PWL(0 0 1 5)`), transient analysis (`.tran 0 1 0 1m`)
- Divider check: at t = 0.5s, V(in) = 2.5V and V(g) = 2.1V (ratio 0.84)

| Model | Current starts (1µA) | Current reaches 1mA | Max current |
|---|---|---|---|
| LTspice library BS170 | ≈ 2.6V | 2.71V | ≈ 111.5mA |
| Threshold set to typical 2.1V | 2.503V | 2.62V | – |

The library model has a higher threshold (≈ 2.28V) than the typical
datasheet value, still within the 0.8–3V range. With the threshold set
to 2.1V, the lamp starts conducting at 2.503V, 0.1% from the design point.

## Limitation
The turn-on is gradual, not sharp: the MOSFET passes through partial
conduction between the threshold and full turn-on. A comparator with
hysteresis would give a clean switch at 2.5V, but it is outside the
allowed parts (one MOSFET and resistors).

## Files
- `brake_light_backup.asc` – LTspice schematic
- `Simulation_Results.pdf` – screenshots and measurements
