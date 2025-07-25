 **complete wiring table** with **Arduino pin numbers**, **connected components**, and their **functions** for **SpeedMath Game** .

---

## Arduino Wiring Table

| Arduino Pin | Connected To                      | Component / Function                              | Notes                                      |
| ----------- | --------------------------------- | ------------------------------------------------- | ------------------------------------------ |
| **D1**      | LCD D7                            | LCD Data Line                                     | 4-bit mode (data pin 4)                    |
| **D2**      | LCD D6                            | LCD Data Line                                     |                                            |
| **D3**      | LCD D5                            | LCD Data Line                                     |                                            |
| **D4**      | LCD D4                            | LCD Data Line                                     |                                            |
| **D5**      | LCD EN                            | LCD Enable                                        | Controls data latching                     |
| **D6**      | LCD RS                            | LCD Register Select                               | Selects instruction/data mode              |
| **D7**      | Keypad Row 1 (R1)                 | Keypad Input                                      | Pulled up via `INPUT_PULLUP`               |
| **D8**      | Keypad Row 2 (R2)                 | Keypad Input                                      |                                            |
| **D9**      | Keypad Row 3 (R3)                 | Keypad Input                                      |                                            |
| **D10**     | Keypad Row 4 (R4)                 | Keypad Input                                      |                                            |
| **D11**     | Keypad Column 1 (C1)              | Keypad Output                                     | Driven LOW during scanning                 |
| **D12**     | Keypad Column 2 (C2)              | Keypad Output                                     |                                            |
| **D13**     | Keypad Column 3 (C3)              | Keypad Output                                     |                                            |
| **A0**      | RESET Pin (via jumper)            | Auto-reset control                                | Used to reset Arduino via code             |
| **A1**      | Buzzer +                          | Passive Buzzer                                    | `tone()` signal is sent here               |
| **A2**      | (Floating/Unconnected)            | Random seed input                                 | Adds entropy for `randomSeed()`            |
| **GND**     | LCD VSS, RW, K, Buzzer -, Pot GND | Ground                                            | Common GND                                 |
| **5V**      | LCD VDD, Pot VCC, etc.            | Power Supply (LCD, Pot, LCD Backlight A via 220Ω) | Use 220Ω in series with backlight (Pin 15) |

---

## LCD Extra Connections

| LCD Pin         | Connected To         | Notes                                         |
| --------------- | -------------------- | --------------------------------------------- |
| **Pin 1 (VSS)** | GND                  | Power ground                                  |
| **Pin 2 (VDD)** | 5V                   | Power supply                                  |
| **Pin 3 (V0)**  | Pot middle pin       | LCD contrast control via 10k potentiometer    |
| **Pin 4 (RS)**  | D6                   | Register select (instruction/data)            |
| **Pin 5 (RW)**  | GND                  | Always LOW for writing                        |
| **Pin 6 (E)**   | D5                   | Enable signal                                 |
| **Pins 11–14**  | D4–D1                | Data lines D4 to D7 in 4-bit mode             |
| **Pin 15 (A)**  | 5V via 220Ω resistor | Backlight anode (with current limit resistor) |
| **Pin 16 (K)**  | GND                  | Backlight cathode                             |

---

## Potentiometer (10k) Wiring – LCD Contrast

| Pot Pin | Connect To     |
| ------- | -------------- |
| Left    | GND            |
| Right   | 5V             |
| Middle  | LCD V0 (Pin 3) |

---


### 220 ohm Resistor

| **Component**  | **Connect To**   | **Notes**                       |
| -------------- | ---------------- | ------------------------------- |
| LCD Pin 15 (A) | 5V via resistor  | Limits current to backlight LED |
| LCD Pin 16 (K) | GND              | Ground connection for backlight |


---

## Passive Buzzer

| Buzzer Pin | Arduino | Notes                   |
| ---------- | ------- | ----------------------- |
| + (VCC)    | A1      | Controlled via `tone()` |
| – (GND)    | GND     | Common ground           |

---

## Reset Jumper

| Arduino A0      | Arduino RESET | Used to restart game on loss             |
| --------------- | ------------- | ---------------------------------------- |
| OUTPUT via code | RESET pin     | Controlled in `loop()` and `check_Ans()` |

---

## A2 Random Seed

| Pin | Function             |                                            |
| --- | -------------------- | ------------------------------------------ |
| A2  | `randomSeed()` input | Leave **unconnected** to read analog noise |

---

## EEPROM Usage (Internal, No Wiring)

| EEPROM Address | Purpose                                     |
| -------------- | ------------------------------------------- |
| `EEPROM[0]`    | Stores high score                           |
| `EEPROM[1]`    | Stores number of restarts to skip animation |

---

## Final Summary

| Pin Group     | Purpose         | Pins Used        |
| ------------- | --------------- | ---------------- |
| LCD           | Display         | D1–D6 + 5V, GND  |
| Keypad        | Input device    | D7–D13           |
| Buzzer        | Audio feedback  | A1               |
| Reset         | Restart circuit | A0 → RESET       |
| EEPROM        | High score save | EEPROM\[0], \[1] |
| Potentiometer | LCD contrast    | GND, 5V, LCD V0  |
| Random Seed   | Randomness      | A2               |

