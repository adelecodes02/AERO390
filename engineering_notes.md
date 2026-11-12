
## Workbook values carried into the model

| Parameter | Value | Source tab | Use |
|---|---:|---|---|
| Roll inertia, Ixx | 181,123.58 kg·m² | Roll Rate | Roll rigid-body plant |
| Bank angle target | 1.04720 rad (60°) | Roll Rate | V&V bank-angle target |
| Time target | 7 s | Roll Rate | V&V bank-time target |
| Required aircraft roll torque | 7,741.72 N·m | Roll Rate | Comparison target |
| Aileron force | 385.16 N | Roll Rate | Estimated aileron roll moment |
| Spoiler force | 192.58 N | Roll Rate | Estimated spoiler roll moment |
| Aileron moment arm | 8.6 m | Roll Rate | Force-to-roll-moment estimate |
| Spoiler moment arm | 5.8 m | Roll Rate | Force-to-roll-moment estimate |
| Aileron hinge moment comparison | 1,560.34 N·m | Superseeded | Aileron hinge-load model |
| Hinge moment coefficient | 0.0150399 | Superseeded | Trace/reference only |
| Hinge load | 10,812.82 N | Superseeded | Trace/reference only |
| Aileron span | 0.740537 m | Inboard Aileron 2D | Geometry metadata |
| Aileron area | 0.341221 m² | Inboard Aileron 2D | Geometry metadata |
| Inboard/outboard aileron chord | 0.486026 / 0.435524 m | Inboard Aileron 2D | Geometry metadata |
| Inboard/outboard hinge arm | 0.145808 / 0.130657 m | Inboard Aileron 2D | Geometry metadata |

## Important consistency check

Using the supplied force and moment-arm values:

- Aileron roll moment = 385.1603 × 8.6 = **3,312.38 N·m**
- Spoiler roll moment = 192.5801 × 5.8 = **1,117.00 N·m**
- Combined estimated roll moment = **4,429.38 N·m**
- Roll torque required by the 60° in 7 s constant-acceleration calculation = **7,741.72 N·m**
- Estimated moment shortfall = **3,312.34 N·m**, or about **42.8%** of the required torque
- Predicted time to 60° from rest using the combined listed surface moments and constant torque = **about 9.25 s**, not 7 s

This is a key V&V finding, not something to tune away. Confirm whether the force values, moment arms, number of surfaces, force allocation, inertia, or roll-time calculation represent the same flight condition and sign convention. The model uses the force × arm values for its first-pass plant and retains the 7 s requirement as a comparison target.

## Assumptions and missing data

1. `qbarScale` is a normalized input from 0 to 1; it is not calibrated to a real airspeed, altitude, Mach number, or dynamic pressure.
2. The 15° travel limit is only a provisional simulation value. The 15° value in the calculation workbook is labelled flap angle and is not proof of the Challenger 3500 aileron/spoiler travel limit.
3. The 20°/s actuator rate and 0.12 s actuator time constant are placeholders, not values calculated from the supplied workbook.
4. A 0.10 m actuator moment arm is a placeholder used only to illustrate hinge-moment-to-force conversion. Replace it with the actual actuator/linkage geometry.
5. The supplied calculation workbook provides an aileron hinge-moment comparison value but no usable spoiler hinge-moment/actuator-load sizing result. `spoilerLoadValid` is therefore set to 0.
6. No validated aerodynamic roll-effectiveness schedule versus Mach, altitude, angle of attack, sideslip, flap setting, or dynamic pressure was supplied.
7. No approved aircraft control laws, actuator architecture, hydraulic pressure/flow data, sensor accuracy, failure-detection timing, or surface travel limits were supplied.
8. The V&V workbook's `Validation Plan` tab is blank. The `Validation` and `Verification Matrix` tabs contain the requirement descriptions and open criteria.

## Interpretation of fault behavior

The FCC logic is deliberately simple and transparent for early V&V:
- Normal: both equivalent differential surfaces command the same roll direction.
- Aileron jam: remove aileron command and retain spoiler command.
- Spoiler jam: remove spoiler command and retain aileron command.
- Both jammed: zero command.

The remaining-authority fractions shown in the model (25.2% spoiler-only and 74.8% aileron-only) are based only on the ratio of the listed force × arm moments. They are not certified controllability results. A jammed surface is held at its last physical position in the simplified plant; its residual aerodynamic effect is not yet included in the roll-moment calculation.


