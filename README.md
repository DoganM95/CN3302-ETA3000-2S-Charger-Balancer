# Intro

A dual cell charger (5V in, 8.4V 4A out) combined with active balancing (1.3A). Highly experimental and untested.

## BOM

### Balancer (2 Amps)

- PC817 (sop-4)
- 0603 1kOhm
- 0603 25kOhm
- 0603 10nF
- 0603 Led red
- 1206 22uF
- 0630 (6.6x6.6x3mm) 2.2uH
- ETA3000 (SOT-23-6)

### Charger (4 Amps)

- 1206 22uF
- 2512 15mOhm
- SS54 (SMA)
- KND3203b (TO-252-2)
- 0603 10kOhm
- CN3302 (sop-8)
- MIC5219-3.3YM5-TR (sot-23-5)
- 0603 10nF

## Schematic

![image](https://github.com/DoganM95/2S-Charge-Balance-Pcb/assets/38842553/f06351ed-6704-4dbe-b4db-51173ba3fcc0)

## Key Takeaways

- The status group of the `ETA3000` consisting of a red led and a 1k resistor use `BatC` as one pole and `SW` as the other. Thus it does not have a real `GND` but current flows with `BatC` acting as Vcc and `SW` acting as `GND` for the led
- The said red status led connections could also be exploited to power an optocoupler, so the `GND` stays independent for this part of the circuit and status becomes measurable using e.g. an arduino
- Connecting `BIAS` or `SW` of the `ETA3000` to the `GND`, which is the negative side of the 2 batteries connected in series, kills the IC and from there it gets very hot while being powered
- None of the 2 ic's (CN3302 && ETA3000) have a symbol in snapeda, so generic packages are used and pins renamed to match this ic

## Resources

### Charger IC: CN3302 (sop-8)

- [Datasheet (EN) of CN3302](https://github.com/DoganM95/2S-Charge-Balance-Pcb/files/13642784/CN3302.zh-CN.en.pdf)
- [Datasheet (CN) of CN3302](https://jlcpcb.com/partdetail/ShangHai_ConsonanceElec-CN3302/C559039)

### Active balancer IC: ETA3000 (sot23-6)
- [Writeup on ETA3000](https://www.beyondlogic.org/review-li-ion-lipo-lifepo4-lithium-battery-active-equalizer-balancer-energy-transfer-board/)
- [Datasheet of ETA3000](https://github.com/DoganM95/2S-Charge-Balance-Pcb/files/13648156/ETA3000-ETA.pdf)
