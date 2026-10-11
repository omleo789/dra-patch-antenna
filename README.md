# Hybrid Patch-DRA Antenna (5-8 GHz)

A broadband hybrid antenna combining a microstrip patch with a stacked dielectric resonator (DRA), designed and simulated in Ansys HFSS for satellite applications. The design target was a fractional bandwidth above 20% across 5-8 GHz.

## Specifications

| Item | Target |
|---|---|
| Frequency range | 5-8 GHz |
| Structure | PCB (patch) + DRA |
| Application | Satellite |
| Bandwidth goal | > 20% (S11 < -10 dB) |
| Measurement | Vector Network Analyzer (VNA) |

## Design

### Geometry
| Parameter | Value |
|---|---|
| Substrate / ground size | 50 x 50 mm |
| Substrate thickness | 1.575 mm |
| Patch (L x W) | 25 x 20 mm |
| Feed | Inset microstrip line, 4.9 mm wide (~50 ohm) |
| Notch gap | 1 mm per side |
| DRA (L x W x H) | 18 x 15 x 7 mm |
| DRA material | er = 9.2, tan d = 0.002 |
| Air gap (patch to DRA) | 0.5 mm |
| Port | 50 ohm lumped port at the substrate edge |
| Boundary | Radiation boundary, 20 mm clearance |

The patch and feedline are modeled as a single zero-thickness PerfectE sheet, and the DRA sits centered above the patch with an air gap. The design is fully parametrized in HFSS, so every dimension above can be swept in Optimetrics.

### How it works
- The patch's length mode (~5.6 GHz) and a second patch mode (~6.6 GHz) give two resonances.
- The DRA, coupled by proximity through the air gap, adds a third resonance near 7.5 GHz and bridges the upper region.
- The inset feed must enter along the patch's resonant (L) direction. Feeding along the wrong edge produced unclear multi-mode behavior early in the project.

## Simulation results

| Band (S11 < -10 dB) | Fractional BW |
|---|---|
| 5.499 - 5.671 GHz | 3.1% |
| 6.541 - 6.829 GHz | 4.3% |
| 7.154 - 7.840 GHz | 9.1% |

Without the DRA, the patch alone shows two deep resonances (~5.55 GHz and ~6.5 GHz) and no third resonance near 7.5 GHz, which confirms the DRA's contribution.

**The >20% continuous-bandwidth target was not met in this version.** Two gaps remain between the resonances:
- ~5.7-6.5 GHz (S11 peaks near -4 dB), caused by the separation between the two patch modes
- ~6.8-7.1 GHz (S11 peaks near -8.5 dB), a smaller gap that comes close to closing

If both gaps closed, the span 5.5-7.8 GHz would give roughly 35% bandwidth.

## Parameter studies

The following were swept to try to close the gaps:

| Parameter | Effect |
|---|---|
| Air gap (0.2-0.8 mm) | Small effect on gap depth |
| Notch gap (0.5-2 mm) | Minimal effect |
| DRA length (14-22 mm) | Moves the upper resonances and closes the smaller gap; no effect on the main gap |
| DRA height / width | Minor effect |
| Patch width (20-24 mm) | Shifts modes, partially reduces the main gap |
| Substrate thickness (1.575-3.14 mm) | Broadens resonances, not enough alone |
| DRA off-center position | No improvement |
| U-slot patch (12 mm gap) | Collapsed to a single resonance; needs further tuning |

The main gap lies between the patch's own two modes, so DRA tuning does not affect it.

## Fabrication

Files in `fabrication/` are for the PCB layer only (patch, feedline and ground).
- The DRA is a separate ceramic block, not part of the Gerber files. It is mounted on the patch after PCB manufacture using a thin foam spacer or adhesive layer.
- The substrate used in simulation must match the substrate ordered from the PCB manufacturer. Check the permittivity before ordering.
- An edge-launch SMA connector is used for VNA measurement.

## Repository structure
