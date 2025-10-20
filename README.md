# Intro

A dual cell charger (3-6V 4A in, 8.4V ~3A out) combined with active balancing (1.3A).   
- The charging part makes sure to load the battery pack to 8.4v
- The balancing part makes sure to keep both batteries at the same voltage always, by charging the lower one using the higher one (active balancing)

Having these combined will in theory give the perfect 2S bms, so that batteries won't die, charge fast and don't waste energy.  

Any buyable bms i have tested so far fails to keep both batteries at the same voltage, so that one is e.g. 4.6v and the other 3.8v, resulting in 8.4v total but leading to damage/death of the overcharged cell, hence this proect to solve the issue and have a reliable, hackable solution.  

Still in concept phase, highly experimental and untested. Even the pcb traces are not wide enough to support the supplied current and would probably delaminate or catch fire.  

Releases starting with v1 or higher can be used and are tested.

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

Most parts a salvaged from commercially available modules, which are dirt-cheap on aliexpress:
- [Charging module (2S, 4A](https://a.aliexpress.com/_EuYAQFK)
- [Balancing module (2S, 1.3A, active)](https://s.click.aliexpress.com/e/_EuIdQJ6)

So all parts of those modules can be desoldered using a hot-plate and solder3d on this project's pcb.

<table>
  <thead>
    <tr>
      <th>Component Symbol</th>
      <th>Size</th>
      <th>Value</th>
      <th>Side Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>C1</td><td>0603</td><td>10nF</td><td></td></tr>
    <tr><td>C2</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C3</td><td>0603</td><td>10nF</td><td></td></tr>
    <tr><td>C4</td><td>0603</td><td>10nF</td><td></td></tr>
    <tr><td>C5</td><td>0603</td><td>10nF</td><td></td></tr>
    <tr><td>C6</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C7</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C8</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C9</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C10</td><td>0603</td><td>10nF</td><td></td></tr>
    <tr><td>C11</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C12</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C13</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>C14</td><td>1206</td><td>22uF</td><td></td></tr>
    <tr><td>D1</td><td>sma</td><td>SS54 (Schottky)</td><td></td></tr>
    <tr><td>L1</td><td>0630 (6.6x6.6x3mm)</td><td>2.2 uH</td><td></td></tr>
    <tr><td>L2 / L3</td><td>any</td><td>2.2 uH</td><td>any that fits there by size</td></tr>
    <tr><td>LED1</td><td>0603</td><td>led</td><td>any color, check R3</td></tr>
    <tr><td>Q1</td><td>TO-252-2</td><td>KND3203b</td><td></td></tr>
    <tr><td>R1</td><td>0603</td><td>5.1 kOhm</td><td></td></tr>
    <tr><td>R2</td><td>0603</td><td>5.1 kOhm</td><td></td></tr>
    <tr><td>R3</td><td>0603</td><td>var Ohm</td><td>choose one that fits your LED1</td></tr>
    <tr><td>R4</td><td>0603</td><td>25 kOhm</td><td></td></tr>
    <tr><td>R5</td><td>2512</td><td>0.015 Ohm</td><td></td></tr>
    <tr><td>R6</td><td>0603</td><td>10 kOhm</td><td></td></tr>
    <tr><td>R7</td><td>0603</td><td>10 kOhm</td><td></td></tr>
    <tr><td>U1</td><td>sot23-6</td><td>ETA3000</td><td></td></tr>
    <tr><td>U2</td><td>smt</td><td>PC817X</td><td></td></tr>
    <tr><td>U3</td><td>sop8</td><td>CN3302</td><td></td></tr>
    <tr><td>U4</td><td>sot23-5</td><td>MIC5219 3.3v</td><td></td></tr>
  </tbody>
</table>

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
