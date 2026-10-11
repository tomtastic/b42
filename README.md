<h1 align="center">B42 battery pack - unlocked</h1>

**B42 Model Label:** `14INR22/71-4`. The arrangement is fourteen series groups of four parallel cells: 56 cells of the 21700 class.

| Label rating | Value | Label rating | Value |
| --- | --- | --- | --- |
| Nominal voltage | 51.66 V | Rated capacity | 18.3 Ah |
| Maximum charge voltage | 58.8 V | Rated energy | 945.37 Wh |
| Maximum charge current | 9.2 A | Maximum discharge current | 36 A |

## Unlock & monitor

Our private utility CLI can :

* **Unlock battery charge/discharge output** through the B42 pack's normal CAN authentication.
* Display live battery telemetry
* Detailed cell voltage and temperature views
* Decoded protection flags
* Switch feedback and JSON logging.

**We will release the CLI at some point in the future.**

## CLI preview

```shell
$ b42_pack.py --bluetooth 00:xx:xx:xx:xx:xx --detailed
B42 node 1  |  2026-10-09T14:55:05.655+00:00
Cached AFE feedback: CHARGE (CHG) DISABLED  DISCHARGE (DSG) DISABLED
Identity: LSBTB420FM_xxxxxxxxxxxxx_  |  [CAN interface redacted]
Firmware 0x00010190  build 0x0077_xx_  model 0x4234_xx_
Stack 47.280 V  PACK 0.210 V
Current -0.010 A  Power -0.47 W  (+ charge / - discharge)
SOC 33.0 %  SOH 95.0 %  Cycles 70 cycles  Discharge estimate n/a
Capacity: remaining 6.011 Ah / full 18.136 Ah / design 18.000 Ah
Gauge: SOC 14.0 %  current 0.000 A
Cells (mV, logical numbering):
  01: 3374  02: 3374  03: 3374  04: 3375  05: 3375  06: 3376  07: 3375
  08: 3376  09: 3378  10: 3380  11: 3380  12: 3380  13: 3383  14: 3384
  Min 3374 mV  max 3384 mV  spread 10 mV  balancing cells none
Temperatures (°C; sensor 2 = gauge; other physical locations unverified):
  1: 21.0  2: 22.0  3: 22.0  4: 22.0
  5: 21.0  6: 21.0  7: 21.0  8: 21.0
Selected temperature 21.0 °C
Advertised charge: 58.80 V, 4.00 A
Dynamic positive-current limit 29.0 A  discharge recommendation 33 (raw)
Mode/session counters: vehicle charge 0 mAh  discharged 0 mAh
Fault summary no
Status: 54=0x0080  58=0x0000  5C=0x0000  60=0x0000  64=0x0008
Flags: presence absent, discharge auth missing
Decoded status flags (cached):
  54: Presence ABSENT [bit 7]  |  Application SOC 20% OR ABOVE [bit 8]  |  Charger detection NOT DETECTED [bit 9]
      Charge temperature inhibit clear [bit 10]  |  Discharge temperature inhibit clear [bit 11]
  58: Overvoltage state clear [bit 0]  |  Undervoltage state clear [bit 1]  |  Idle inhibit clear [bit 15]
  5C: CHARGE (CHG) DISABLED [bit 13]  |  DISCHARGE (DSG) DISABLED [bit 14]  |  Fault summary clear [bit 15]
  60: Balancing cells none
  64: Discharge authentication MISSING [bit 3]  |  Predischarge retry failure clear [bit 5]
      Excessive PACK voltage clear [bit 11]  |  Precharge inactive [bit 12]
```

```shell
$ b42_pack.py --bluetooth 00:xx:xx:xx:xx:xx --mode discharge --detailed
B42 node 1  |  2026-10-11T13:35:29.494+00:00
Cached AFE feedback: CHARGE (CHG) ENABLED  DISCHARGE (DSG) ENABLED
Identity: LSBTB420FM_xxxxxxxxxxxxx_  |  [CAN interface redacted]
Firmware 0x00010190  build 0x0077_xx_  model 0x4234_xx_
Stack 47.250 V  PACK 47.240 V
Current -0.010 A  Power -0.47 W  (+ charge / - discharge)
SOC 14.0 %  SOH 95.0 %  Cycles 70 cycles  Discharge estimate n/a
Capacity: remaining 2.528 Ah / full 18.252 Ah / design 18.000 Ah
Gauge: SOC 16.0 %  current 0.000 A
Cells (mV, logical numbering):
  01: 3371  02: 3371  03: 3370  04: 3372  05: 3372  06: 3373  07: 3373
  08: 3374  09: 3375  10: 3376  11: 3378  12: 3377  13: 3380  14: 3381
  Min 3370 mV  max 3381 mV  spread 11 mV  balancing cells none
Temperatures (°C; sensor 2 = gauge; other physical locations unverified):
  1: 22.0  2: 23.0  3: 22.0  4: 22.0
  5: 22.0  6: 22.0  7: 22.0  8: 22.0
Selected temperature 22.0 °C
Advertised charge: 58.80 V, 4.00 A
Dynamic positive-current limit 29.0 A  discharge recommendation 25 (raw)
Mode/session counters: vehicle charge 0 mAh  discharged 0 mAh
Fault summary no
Status: 54=0x0100  58=0x0000  5C=0x6000  60=0x0000  64=0x0000
Flags: application SOC below 20%
Decoded status flags (cached):
  54: Presence PRESENT [bit 7]  |  Application SOC BELOW 20% [bit 8]  |  Charger detection NOT DETECTED [bit 9]
      Charge temperature inhibit clear [bit 10]  |  Discharge temperature inhibit clear [bit 11]
  58: Overvoltage state clear [bit 0]  |  Undervoltage state clear [bit 1]  |  Idle inhibit clear [bit 15]
  5C: CHARGE (CHG) ENABLED [bit 13]  |  DISCHARGE (DSG) ENABLED [bit 14]  |  Fault summary clear [bit 15]
  60: Balancing cells none
  64: Discharge authentication PRESENT [bit 3]  |  Predischarge retry failure clear [bit 5]
      Excessive PACK voltage clear [bit 11]  |  Precharge inactive [bit 12]
```

State Of Charge (SOC), State Of Health (SOH) and capacities are drawn directly from the B42 telemetry.

## Pack & connector

<p align="center">
  <img height="260" alt="B42 external connector face" src="https://github.com/user-attachments/assets/2994a7c3-bdd9-4ac9-aa16-fae0bf856b96" />
  &nbsp;
  <img height="260" alt="External connector wiring" src="https://github.com/user-attachments/assets/43362316-3eeb-4b6c-ab40-e9a65a86fa48" />
  <br><sub>Connector face · Connector wiring</sub>
</p>

| Pin | Colour | Function |
| --- | --- | --- |
| + | Red | Switched pack positive |
| − | Black | Pack negative |
| 1 | Yellow | ECU: pack-controlled pulsed signal |
| 2 | Green | CAN-H |
| 3 | Blue | CAN-L |
| 4 | White | DET: active-low wake/presence input |

PCB signal wires run top-to-bottom yellow, green, blue, white in the board image. ECU's driver circuitry, electrical limits and external receiver remain unresolved. DET asserts presence when pulled low.

## Control board

**PCB:** `LB42ST-A03` · Numbers identify components; dashed sections indicate proposed functions.

<p align="center"><a href="board-merged-annotated.jpg"><img width="880" alt="Annotated B42 board with component numbers and proposed functional sections" src="board-merged-annotated.jpg" /></a><br><sub>Open the image for full-resolution annotations.</sub></p>

| Map | Reference | Component / role |
| --- | --- | --- |
| 1 | U300 | STM32G0B1RCT6 microcontroller; firmware and communications |
| 2 | U100 | TI BQ76952; monitoring, balancing and protection |
| 3 | U800 | TI BQ34Z100-family fuel gauge; revision unconfirmed |
| 4 | U400 | TI TCAN1042-family CAN transceiver with VIO |
| 5 | Q103 | NCE0110AK MOSFET; circuit role unresolved |
| 6 | F200 | Dexerials SFK-5045A, 45 A protection fuse |
| 7 | Q206? | NCEP029N10D power MOSFET; reference tentative |

Functional groupings and labelled SWD/I²C access are inferred from visible parts and routing. B1–B13 mark intermediate cell-stack connections; B− and B+ are the ends. Full wiring remains unverified.

## CAN interface

**Classic CAN · 250 kbit/s · Standard 11-bit identifiers**

Periodic reports and on-demand reads expose pack/cell voltages, currents, temperatures, SOC/SOH, design/full/remaining capacities, cycles, balancing, protection flags, charge/discharge feedback, identity and recorded voltage/current/temperature extrema. Recorded extrema do not establish a complete lifetime fault history.

Charging and discharge have separate qualifying conditions. For discharge authentication, the pack supplies a challenge; the controller calculates a reply using repeated arithmetic and bit mixing; the pack compares it with its expected answer. A match satisfies the authentication condition, with firmware protections still governing permission.
