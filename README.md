# Hybrid Patch-DRA Antenna (5-8 GHz)

Broadband patch + dielectric resonator antenna designed in Ansys HFSS
for satellite applications. Target: fractional bandwidth > 20%.

## Specifications
- Frequency range: 5-8 GHz
- Structure: PCB (patch) + DRA
- Measurement: VNA
- Target: BW > 20%

## Design
| Parameter | Value |
|---|---|
| Substrate | Rogers RT/duroid 5880 (er=2.2, h=1.575 mm) |
| Substrate/ground size | 50 x 50 mm |
| Patch (L x W) | 25 x 20 mm |
| Feed | Inset microstrip line, 4.9 mm (50 ohm) |
| DRA | 18 x 15 x 7 mm, er=9.2, tan d=0.002 |
| Air gap | 0.5 mm |

## Results (HFSS simulation)
| Band (-10 dB) | Fractional BW |
|---|---|
| 5.499 - 5.671 GHz | 3.1% |
| 6.541 - 6.829 GHz | 4.3% |
| 7.154 - 7.840 GHz | 9.1% |

The DRA adds a third resonance near 7.5 GHz, but a gap between
the two patch modes (~5.7-6.5 GHz) prevents one continuous band.

## Design notes
- Feed must enter along the patch's resonant (L) direction
- Parameter sweeps tried: air_gap, notch_gap, dra_l/h/w, patch_W, sub_H
- Next step: U-slot or E-shaped patch to merge the two patch modes

## Files
- `hfss/` HFSS project
- `results/` S11 plots
- `fabrication/` DXF and Gerber files
