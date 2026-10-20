# Data format

Participant data is not included in this repository to protect participant privacy.

The notebook expects one CSV file per participant in `DATA_DIR`. File names are not used in any output: participants are assigned anonymous IDs (P01, P02, ...) in sorted file order.

Each file is the raw log from the Spondon device and contains two kinds of lines.

**Sensor lines** (about one per second), 11 comma-separated values:

| Column | Description |
|---|---|
| `Time` | Clock time, `HH:MM:SS` |
| `HR_Red`, `HR_IR` | Raw MAX30102 red and infrared PPG values |
| `Inst_BPM` | Instantaneous heart rate (beats per minute) |
| `GSR_Raw` | Raw ADC reading from the GSR sensor |
| `GSR_uS` | Skin conductance (µS) |
| `BodyTemp_C` | Peripheral body temperature (°C) |
| `AmbientTemp_C` | Ambient temperature (°C) |
| `ACC_X_G`, `ACC_Y_G`, `ACC_Z_G` | Acceleration (g) |

Example:
```
10:00:01, 54210, 55873, 82.4, 610, 1830.5, 26.12, 29.50, 0.01, -0.02, 0.98
```

**HRV summary lines** (about one per minute), `key: value` pairs that include `HRV_available` and `RMSSD`:
```
HRV_available: true, RMSSD: 78.41, SDNN: 94.10, pNN50: 23.5
```

Phases are assigned from elapsed time since the first sensor line: 0–300 s Baseline, 300–600 s Stroop Test, after 600 s Recovery.
