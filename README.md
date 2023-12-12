# 2S-Charge-Balance-Pcb
A dual cell charger (5V in, 8.4V 4A out) combined with active balancing (1.3A)


## BOM
The parts list so far as a list, so they can be ordered from aliexpress:

### Balancer
- PC817 (sop-4)
- 0603 1kOhm
- 0603 25kOhm
- 0603 10nF
- 0603 Led red
- 1206 22uF
- 0630 (6.6x6.6x3mm) 2.2uH
#### Deprecated
- 0603 1nF

## Key Takeaways
- The status group of the `ETA3000` consisting of a red led and a 1k resistor use `BatC` as one pole and `SW` as the other. Thus it does not have a real `GND` but current flows with `BatC` acting as Vcc and `SW` acting as `GND` for the led
- The said red status led connections could also be exploited to power an optocoupler, so the `GND` stays independent for this part of the circuit and status becomes measurable using e.g. an arduino
- Connecting `BIAS` or `SW` of the `ETA3000` to the `GND`, which is the negative side of the 2 batteries connected in series, kills the IC and from there it gets very hot while being powered
