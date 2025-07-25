# Arduino-SpeedMaths-Game

Here’s a **detailed explanation** of how the **SpeedMath Game** (also called *Mathopia* or *Arduino Speed Math Olympiad Game*) works — both in terms of **electronics and programming**.

---

##  Concept Overview

**SpeedMath Game** challenges your ability to solve math problems quickly, under pressure. It works by displaying random math questions on an LCD, accepting user input via a keypad, and giving audio-visual feedback using a passive buzzer and display messages.

---

##  Step-by-Step Working

### 1. **Startup and Initialization**

* When the Arduino starts, it:

  * Initializes the **LCD**, **keypad**, and **buzzer**.
  * Seeds the random number generator using analog noise from an unconnected analog pin (A2).
  * Displays a **welcome message** and shows the **high score** stored in EEPROM.
  * Waits for a button press on the keypad to begin the game.

---

### 2. **Game Flow**

####  Random Math Question

* The game randomly selects a **question** from a preloaded list of 20 math problems stored in an array.
* Each question has a **predefined correct answer** stored in a separate array.

####  Question Display

* The selected question is printed on the **LCD screen**.
* A **10-second timer** starts (using `millis()` function).

####  User Input

* The user inputs their answer using a **4x3 matrix keypad**.
* Numbers are captured into a `keypad[]` array.
* The `-` key sets the number as negative (if required).
* Once the user presses the "Enter" key (bottom right key), the system:

  * Combines the digits into a number.
  * Compares the user input with the correct answer.

---

### 3. **Feedback and Scoring**

#### Correct Answer:

* LCD shows: `Correct!`
* Score counter (`solcounter`) increases by 1.
* A success **tone sequence** is played using the **passive buzzer**.

#### Wrong Answer or Timeout:

* LCD shows: `Wrong Answer` or `Out of Time`
* The game ends immediately.
* The current score is displayed.
* If it’s a new high score, it updates **EEPROM\[0]**.
* A distinct **failure tone sequence** plays using the buzzer.

---

### 4. **Game Reset Logic**

* After game over (wrong or timeout), the Arduino **resets itself** using:

  * A software-triggered signal from pin **A0** connected physically to the **RESET** pin.
* Before reset, EEPROM\[1] is updated to avoid the welcome animation running repeatedly on restarts.

---

## Passive Buzzer Tone Generation

A **passive buzzer** works by receiving PWM signals (square waves) from the Arduino's `tone()` function.

### Frequency to Sound Mapping:

| Note | Frequency (Hz) | Tone Used In Game |
| ---- | -------------- | ----------------- |
| Do   | 523 Hz         |   (Correct)       |
| Re   | 587 Hz         |   (Wrong)         |
| Mi   | 659 Hz         |    (Melody)       |

By sending square wave pulses of certain frequencies and durations, the Arduino makes the buzzer vibrate at different speeds — producing different musical tones.

For example:

```cpp
tone(BUZZER, 523, 300); // Play “Do” for 300 milliseconds
```

This tone sequence gives **audio feedback** to make the game more engaging.

---

## Game Features Summary

| Feature          | How it Works                                  |
| ---------------- | --------------------------------------------- |
| Random Questions | From a 20-question array using `random()`     |
| Time Limit       | 10 seconds via `millis()` comparison          |
| Answer Input     | Keypad entries stored in an array             |
| Audio Feedback   | Tones using passive buzzer                    |
| Visual Feedback  | LCD messages like "Correct!" or "Out of Time" |
| Score Tracking   | Variable + EEPROM storage                     |
| Game Reset       | Pin A0 connected to RESET pin                 |

---

## Educational Value

This project teaches:

* **Basic math logic** and problem-solving under pressure.
* How to work with **LCDs**, **keypads**, **EEPROM**, and **buzzers**.
* How to use **millis()**, `tone()`, `random()`, and `EEPROM` in Arduino programming.
* How to combine **hardware + software** for interactive systems.

---

Would you like me to format this as a **README.md** section too, for uploading to GitHub?
