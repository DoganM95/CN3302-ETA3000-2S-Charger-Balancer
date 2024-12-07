# Intro

A dual cell charger (3-6V in, 8.4V 4A out) combined with active balancing (1.3A).   
- The charging part makes sure to load the battery pack to 8.4v
- The balancing part makes sure to keep both batteries at the same voltage always, by charging the lower one using the higher one (active balancing)

Having these combined will in theory give the perfect 2S bms, so that batteries won't die, charge fast and don't waste energy.  

Any buyable bms i have tested so far fails to keep both batteries at the same voltage, so that one is e.g. 4.6v and the other 3.8v, resulting in 8.4v total but leading to damage/death of the overcharged cell, hence this proect to solve the issue and have a reliable, hackable solution.  

Highly experimental and untested. Releases starting with v1 or higher can be used and are tested.

# PCB

<table>
  <tr>
    <td>
      <img src="https://github.com/DoganM95/CN3302-ETA3000-2S-Charger-Balancer/blob/master/assets/top.png?raw=true" alt="PCB Top View"/>
    </td>
    <td>
      <img src="https://github.com/DoganM95/CN3302-ETA3000-2S-Charger-Balancer/blob/master/assets/bottom.png?raw=true" alt="PCB Bottom View"/>
    </td>
  </tr>
</table>

## BOM

Schema: Component Symbol, size, value, side-notes
- C1: 0603 10nF
- C2: 1206 22uF
- C3: 0603 10nF
- C4: 0603 10nF
- C5: 0603 10nF
- C6: 1206 22uF
- C7: 1206 22uF
- C8: 1206 22uF
- C9: 1206 22uF
- C10: 0603 10nF
- C11: 1206 22uF
- C12: 1206 22uF
- C13: 1206 22uF
- C14: 1206 22uF
- D1: sma SS54 (Schottky)
- L1: 0630 (6.6x6.6x3mm) 2.2 uH
- L2 / L3: any 2.2 uH that fits there by size
- LED1: 0603 led (any color, check R3)
- Q1: KND3203b (TO-252-2)
- R1: 0603 5.1 kOhm
- R2: 0603 5.1 kOhm
- R3: 0603 var Ohm (choose one that fits your LED1)
- R4: 0603 25 kOhm
- R5: 2512 0.015 Ohm
- R6: 0603 10 kOhm
- R7: 0603 10 kOhm
- U1: sot23-6 ETA3000
- U2: smt PC817X
- U3: sop8 CN3302
- U4: sot23-5 MIC5219 3.3v

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
