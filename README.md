<div align="center">

<!-- HEADER BANNER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0D1B2A,1B3A5C,2E6DA4&height=200&section=header&text=24-Hour%20Digital%20Logic%20Clock&fontSize=36&fontColor=ffffff&fontAlignY=38&desc=Hardware-Based%20Implementation%20Using%20Digital%20Logic%20ICs&descAlignY=56&descColor=4A9FD4&animation=fadeIn" alt="Project Banner" width="100%"/>

<!-- BADGES -->
<p>
  <img src="https://img.shields.io/badge/Status-Completed-2E6DA4?style=for-the-badge&logo=checkmarx&logoColor=white" alt="Status"/>
  <img src="https://img.shields.io/badge/Platform-Breadboard-C9A84C?style=for-the-badge&logo=arduino&logoColor=white" alt="Platform"/>
  <img src="https://img.shields.io/badge/Format-24--Hour-0D1B2A?style=for-the-badge&logo=clockify&logoColor=white" alt="Format"/>
  <img src="https://img.shields.io/badge/ICs-74LS%20Series-2E6DA4?style=for-the-badge&logo=raspberrypi&logoColor=white" alt="ICs"/>
  <img src="https://img.shields.io/badge/Display-7--Segment%20LED-C9A84C?style=for-the-badge&logo=led&logoColor=white" alt="Display"/>
  <img src="https://img.shields.io/badge/Course-Digital%20Logic%20Design-1B3A5C?style=for-the-badge" alt="Course"/>
</p>

<p>
  <strong>Zewail City of Science and Technology — Faculty of Engineering & Applied Sciences</strong><br/>
  <em>Digital Logic Design Course Project · Spring 2026</em>
</p>

---

</div>

## 📋 Table of Contents

| # | Section | # | Section |
|---|---------|---|---------|
| 1 | [Project Overview](#-project-overview) | 9 | [Project Images](#-project-images) |
| 2 | [Features](#-features) | 10 | [Demonstration Video](#-demonstration-video) |
| 3 | [Hardware Components](#-hardware-components) | 11 | [Challenges Faced](#-challenges-faced) |
| 4 | [System Architecture](#-system-architecture) | 12 | [Future Improvements](#-future-improvements) |
| 5 | [How the Clock Works](#-how-the-clock-works) | 13 | [Repository Structure](#-repository-structure) |
| 6 | [Circuit Design](#-circuit-design) | 14 | [Team Members](#-team-members) |
| 7 | [Working Principle](#-working-principle) | 15 | [Conclusion](#-conclusion) |
| 8 | [Clock Generation & Timing](#%EF%B8%8F-clock-generation--timing-logic) | 16 | [References](#-references) |

---

## 🔭 Project Overview

This project is a **fully hardware-based 24-hour digital clock** designed and implemented entirely from discrete **digital logic integrated circuits (ICs)** on a breadboard — with **no microcontrollers, no FPGAs, and no software**.

The clock accurately displays time in **HH:MM:SS** format (Hours : Minutes : Seconds) across **six 7-segment LED displays**, counting from `00:00:00` to `23:59:59` and rolling over automatically. The system is powered by a **555 Timer IC** astable oscillator generating a stable **1 Hz clock signal**, which drives a cascade of **BCD decade counters** with **combinational reset logic** enforcing the 24-hour time boundary.

> **Engineering Philosophy:** Every digit on the display, every count, every reset — is handled purely by transistor-level logic gates, flip-flops, and counters. This project is a living demonstration of how all modern timekeeping began.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SYSTEM SIGNAL FLOW                                   │
│                                                                         │
│  [555 Timer] ──1Hz──► [Seconds Counter] ──► [Minutes Counter]          │
│                              │                      │                   │
│                         Mod-60 Reset           Mod-60 Reset             │
│                              │                      │                   │
│                              └──────────────────────►[Hours Counter]   │
│                                                            │            │
│                                                      Mod-24 Reset       │
│                              ▼                       ▼         ▼        │
│                         [74LS47 ×6]  BCD→7-Seg Decoders                │
│                              ▼                                          │
│                    [ HH : MM : SS ]  7-Segment LED Displays             │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features

<table>
<tr>
<td width="50%">

**⏱️ Core Functionality**
- ✅ Full **24-hour time format** (00:00:00 → 23:59:59)
- ✅ Automatic roll-over at midnight (`23:59:59 → 00:00:00`)
- ✅ Accurate **1 Hz clock** generation via 555 Timer
- ✅ Six **7-segment LED displays** for HH:MM:SS readout
- ✅ Manual **hours and minutes setting** via push-buttons
- ✅ **No microcontroller** — pure hardware logic

</td>
<td width="50%">

**🔧 Hardware Highlights**
- ✅ Cascaded **BCD Modulo-60** counter pairs (seconds, minutes)
- ✅ **Modulo-24** hours counter with combinational reset
- ✅ **74LS47 BCD-to-7-Segment** decoder/driver ICs
- ✅ **74LS90 decade counters** with synchronous cascade
- ✅ NAND/AND gate reset logic for non-power-of-2 moduli
- ✅ Decoupling capacitors for supply noise suppression

</td>
</tr>
</table>

---

## 🔩 Hardware Components

### Bill of Materials (BOM)

| # | Component | Designation | Function | Qty | Specification |
|:-:|-----------|:-----------:|----------|:---:|---------------|
| 1 | **555 Timer IC** | NE555 / LM555 | Astable 1 Hz clock generator | 1 | VCC = 5V, fout ≈ 1 Hz |
| 2 | **BCD Decade Counter** | 74LS90 / CD4518 | Modulo-10 & Modulo-6 cascaded counting | 6 | 4-bit BCD, synchronous reset |
| 3 | **BCD-to-7-Seg Decoder** | 74LS47 | Decode BCD → 7-segment signals | 6 | Active-low outputs, common-anode |
| 4 | **7-Segment Display** | 5611BS | Visual numeric output — HH:MM:SS | 6 | Common-anode, red LED |
| 5 | **NAND Gate IC** | 74LS00 | Combinational reset detection logic | 2 | Quad 2-input NAND |
| 6 | **AND Gate IC** | 74LS08 | Carry propagation & modulo detection | 1 | Quad 2-input AND |
| 7 | **Resistors** | 330 Ω – 10 kΩ | Current limiting, 555 timing network | ~20 | 1/4 W, 5% tolerance |
| 8 | **Electrolytic Capacitor** | 10 µF / 100 µF | 555 RC timing & bulk decoupling | 2 | 25V, polarized |
| 9 | **Ceramic Capacitor** | 0.01 µF | VCC bypass at each IC pin | 4 | 50V, non-polarized |
| 10 | **Push-Button Switch** | SPST Tactile | Manual hours / minutes set | 2 | Momentary, NO contact |
| 11 | **Potentiometer** | 10 kΩ | Fine-tune oscillator frequency | 1 | Linear taper |
| 12 | **LED Indicator** | Red LED | Power-on status indicator | 1 | VF ≈ 2V, 20 mA max |
| 13 | **Breadboard** | MB-102 | Prototyping platform | 1 | 830 tie-points |
| 14 | **DC Power Supply** | 5V regulated | System VCC | 1 | 5.0V ±5%, ≥500 mA |
| 15 | **Jumper Wires** | 22 AWG solid | Breadboard interconnections | ~100 | Color-coded |

---

## 🏗️ System Architecture

The system is organized into **five distinct functional layers**, each with clearly defined inputs and outputs:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                         SYSTEM ARCHITECTURE                                  │
│                                                                              │
│  ┌─────────────────┐                                                         │
│  │   LAYER 1       │   NE555 in Astable Mode                                 │
│  │  Timing / OSC   │   RC Network: RA=47kΩ, RB=68kΩ+10kΩ pot, CT=10µF      │
│  │  1 Hz Clock     │   Output: Stable 1 Hz square wave                      │
│  └────────┬────────┘                                                         │
│           │ 1 Hz CLK                                                         │
│  ┌────────▼────────┐                                                         │
│  │   LAYER 2       │   74LS90 ×6 (three pairs)                              │
│  │  Counting Layer │   Pair 1: Seconds  → Mod-60 (00–59)                    │
│  │  BCD Counters   │   Pair 2: Minutes  → Mod-60 (00–59)                    │
│  │                 │   Pair 3: Hours    → Mod-24 (00–23)                    │
│  └────────┬────────┘                                                         │
│           │ BCD[7:0] per field                                               │
│  ┌────────▼────────┐                                                         │
│  │   LAYER 3       │   74LS00 (NAND) + 74LS08 (AND)                        │
│  │  Reset Logic    │   Detects: SS=60 → CLR seconds + carry                 │
│  │  Combinational  │   Detects: MM=60 → CLR minutes + carry                 │
│  │                 │   Detects: HH=24 → CLR hours (Mod-24 wrap)             │
│  └────────┬────────┘                                                         │
│           │ Segment drive signals                                            │
│  ┌────────▼────────┐                                                         │
│  │   LAYER 4       │   74LS47 ×6                                            │
│  │  Decoding Layer │   BCD (4-bit) → 7-segment (a–g)                        │
│  │  BCD → 7-Seg    │   Active-low outputs for common-anode displays          │
│  └────────┬────────┘                                                         │
│           │ a,b,c,d,e,f,g per digit                                          │
│  ┌────────▼────────┐                                                         │
│  │   LAYER 5       │   5611BS ×6 (Common-Anode LED)                         │
│  │  Display Layer  │   330Ω current-limiting resistors per segment           │
│  │  HH : MM : SS   │   Segment current ≈ 9 mA per segment                   │
│  └─────────────────┘                                                         │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ How the Clock Works

### The Core Counting Chain

```
1 Hz Pulse
    │
    ▼
[SC0] Seconds Ones (0–9)
    │ carry (falling edge of QD)
    ▼
[SC1] Seconds Tens (0–5) ──► AND(QB, QC) = 1? ──► CLR both + carry to minutes
    │
    ▼
[MC0] Minutes Ones (0–9)
    │ carry
    ▼
[MC1] Minutes Tens (0–5) ──► AND(QB, QC) = 1? ──► CLR both + carry to hours
    │
    ▼
[HC0] Hours Ones (0–9)
    │ carry
    ▼
[HC1] Hours Tens (0–2) ──► AND(HC1.QB, HC0.QC) = 1? ──► CLR both → 00:00:00
```

### Key Design Decisions

| Design Choice | Reason |
|---------------|--------|
| **Modulo-60 via AND(QB, QC)** | State 6 = `0110` in BCD; QB=1 and QC=1 uniquely identifies it |
| **Modulo-24 via AND(HC1.QB, HC0.QC)** | State 24 = `0010 0100`; cross-field detection required |
| **Ripple carry between ones → tens** | Falling edge of QD triggers next counter; acceptable at 1 Hz |
| **74LS47 with active-low outputs** | Directly compatible with common-anode 5611BS displays |
| **330Ω segment resistors** | Limits segment current to ~9 mA; safe for IC and display |

---

## 🔌 Circuit Design

### 555 Timer — Astable Oscillator

The 555 Timer is configured in **astable mode** to generate a continuous 1 Hz square wave:

```
              VCC (+5V)
               │
        RA     │
       ┌─┤47kΩ├─┤
       │       │
       │  RB   ├── Pin 7 (DISCHARGE)
       └─┤68kΩ├─┤
       │ (+ pot)│
       │       ├── Pin 6 (THRESHOLD)
       │       ├── Pin 2 (TRIGGER)
       │  CT   │
       └─┤10µF├─┤
               │
              GND

  Frequency:  f = 1.44 / ((RA + 2·RB) · CT)
            ≈ 1.44 / ((47k + 2×68k) · 10µ)
            ≈ 1.00 Hz  ✓

  Duty Cycle: D = (RA + RB) / (RA + 2·RB) ≈ 59%
```

### BCD Counter Cascade — Modulo-60 Example (Seconds)

```
CLK ──►[CLK A]─[74LS90 SC0]─[QA]──►[CLK B]   ← Ones digit (0–9)
              [QD] ─────────────────────────────►[CLK A]─[74LS90 SC1] ← Tens digit
                                                 [QB]─┐
                                                 [QC]─┴──►[AND Gate]──►[R0(1), R0(2)]
                                                          Reset at 6 (=0110)
                                                          → CLR both SC0 & SC1
                                                          → Carry pulse to minutes
```

### Modulo-24 Reset Logic (Hours)

```
HC1[QB] ─┐
          ├──►[2-input AND]──► CLR signal ──► HC0.R0(1,2)
HC0[QC] ─┘                                   HC1.R0(1,2)
   │                                          Resets HH to 00
   Detection of decimal 24:
   HC1 = 0010 → QB = 1
   HC0 = 0100 → QC = 1
   Combined: AND = 1 → instant reset
```

---

## ⚡ Clock Generation & Timing Logic

### Oscillator Component Selection

| Parameter | Symbol | Value | Notes |
|-----------|:------:|-------|-------|
| Timing Resistor A | RA | 47 kΩ | Fixed carbon film |
| Timing Resistor B | RB | 68 kΩ + 10 kΩ pot | ±5% fine trim range |
| Timing Capacitor | CT | 10 µF | Electrolytic, 25V |
| Output Frequency | fout | ≈ 1.00 Hz | Verified vs. stopwatch |
| HIGH Period | tH | ≈ 592 ms | Charge path: RA + RB |
| LOW Period | tL | ≈ 408 ms | Discharge path: RB only |
| Duty Cycle | D | ≈ 59% | Acceptable for counter CLK |
| Supply Bypass Cap | — | 0.01 µF | On pin 5 (Control Voltage) |

> **Accuracy note:** RC-based 555 oscillators achieve ±5% frequency accuracy. Over 24 hours, this equates to a maximum drift of ±72 minutes. For educational purposes, this is acceptable; see [Future Improvements](#-future-improvements) for precision enhancement.

---

## 🔬 Working Principle

### Step-by-Step State Machine

```
POWER ON → All counters initialize to 00:00:00
    │
    ▼
Every 1 second (rising edge of 1 Hz clock):
    │
    ├── SC0 increments (0→1→...→9)
    │       │ [at 9→0 transition]
    │       ▼
    │   SC1 increments (0→1→...→5)
    │       │ [at SC1=6 detected by AND gate]
    │       ▼
    │   RESET SC0 + SC1 → 00 (seconds = 00)
    │   GENERATE carry pulse → clock MC0
    │
    ├── MC0 increments (0→1→...→9)
    │       │ [at 9→0 transition]
    │       ▼
    │   MC1 increments (0→1→...→5)
    │       │ [at MC1=6 detected by AND gate]
    │       ▼
    │   RESET MC0 + MC1 → 00 (minutes = 00)
    │   GENERATE carry pulse → clock HC0
    │
    └── HC0 increments (0→1→...→9)
            │ [at 9→0 transition]
            ▼
        HC1 increments (0→2)
            │ [at HC1.QB AND HC0.QC = 1 → state 24 detected]
            ▼
        RESET HC0 + HC1 → 00 (hours = 00)
        → Display shows 00:00:00 ← MIDNIGHT ROLLOVER
```

### 74LS47 BCD-to-7-Segment Truth Table

| Digit | D | C | B | A | a | b | c | d | e | f | g |
|:-----:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **0** | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| **1** | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |
| **2** | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 |
| **3** | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
| **4** | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 |
| **5** | 0 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 0 |
| **6** | 0 | 1 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| **7** | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 1 |
| **8** | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **9** | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |

> Output `0` = segment **ON** (active-low), Output `1` = segment **OFF**

---

## 🖼️ Project Images

### Breadboard Implementation

<div align="center">

<!-- Replace with your actual image path -->
![Digital Clock Breadboard Implementation](assets/images/breadboard_full.jpg)

*Complete breadboard implementation — six 7-segment displays (top), BCD decoder ICs (upper middle), counter ICs (lower middle), 555 Timer oscillator and push-button controls (bottom)*

</div>

### Close-Up Views

<div align="center">

| Display Section | Counter & Decoder ICs | Oscillator Circuit |
|:-:|:-:|:-:|
| ![Display](assets/images/display_closeup.jpg) | ![ICs](assets/images/ic_section.jpg) | ![Oscillator](assets/images/oscillator.jpg) |
| *Six 5611BS 7-segment displays showing HH:MM:SS* | *74LS90 counters and 74LS47 decoders* | *555 Timer RC network with potentiometer* |

</div>

> 📸 **Note:** Replace placeholder paths with actual image files placed in `assets/images/`.

---

## 🎬 Demonstration Video

<div align="center">

<!-- Replace with actual video thumbnail and link -->
[![24-Hour Digital Clock Demo](assets/images/video_thumbnail.jpg)](assets/videos/clock_demo.mp4)

*▶️ Click to watch the full demonstration — showing 00:00:00 to 23:59:59 rollover, manual time setting, and real-time counting*

</div>

> 🎥 **Note:** Place your demonstration video at `assets/videos/clock_demo.mp4`, or link to a YouTube/Google Drive upload.

---

## ⚠️ Challenges Faced

<details>
<summary><strong>Challenge 1: Inaccurate Clock Frequency (555 Timer drift)</strong></summary>

**Problem:** Initial RC component values produced ~0.85 Hz due to resistor/capacitor tolerance stack-up, causing the clock to run fast by approximately 8 minutes per hour.

**Solution:** Added a 10 kΩ potentiometer in series with RB for continuous fine-tuning. Frequency was calibrated against a mobile phone stopwatch over a 10-minute window. Final measured frequency: **1.00 ± 0.02 Hz**.

</details>

<details>
<summary><strong>Challenge 2: Spurious Display of "24" on Hours Roll-Over</strong></summary>

**Problem:** Without sufficient analysis of gate propagation delay, concerns arose that the counters would briefly pass through state `24` before reset logic fired, causing a visible flicker.

**Solution:** Measured total reset propagation delay of 74LS NAND + AND gate chain: **< 50 ns**. Since the clock period is 1 second, the state `24` persists for < 50 ns — physically invisible. No additional latching circuitry required.

</details>

<details>
<summary><strong>Challenge 3: Wiring Density and Short Circuits</strong></summary>

**Problem:** Over 100 jumper wires created a high-density breadboard where accidental short circuits, particularly on power rails, caused erratic counter behavior and false resets.

**Solution:** Implemented a strict **color-coding convention**:
- 🔴 Red → VCC (+5V)
- ⚫ Black → GND
- 🟡 Yellow → Clock signals
- 🟠 Orange → BCD data lines
- ⚪ Gray → Reset / CLR lines

Each functional section was wired and tested independently before integration.

</details>

<details>
<summary><strong>Challenge 4: Counter Skipping States (Bad Breadboard Contact)</strong></summary>

**Problem:** One 74LS90 occasionally skipped count states, displaying incorrect digits. Traced to an intermittent breadboard contact on the CLK A pin under thermal expansion.

**Solution:** Replaced the affected breadboard rows with fresh tie-points and ensured solid wire seating. Issue fully resolved after re-seating.

</details>

<details>
<summary><strong>Challenge 5: LED Segment Overheating</strong></summary>

**Problem:** Initial 220 Ω segment resistors produced ~14 mA per segment — near the maximum rated current — causing noticeable component heating over prolonged operation.

**Solution:** Replaced all segment resistors with **330 Ω**, reducing segment current to **~9 mA** while maintaining clearly visible display brightness.

</details>

<details>
<summary><strong>Challenge 6: Power Supply Noise Causing False Counter Triggers</strong></summary>

**Problem:** High-frequency switching transients on the VCC rail caused occasional false clock edges on counter inputs, resulting in double-counting artifacts.

**Solution:** Added **100 µF electrolytic capacitors** at both power rails for bulk decoupling, and **0.1 µF ceramic capacitors** at the VCC pin of every IC. False triggering was eliminated entirely.

</details>

---

## 🚀 Future Improvements

| Priority | Improvement | Impact |
|:--------:|-------------|--------|
| 🔴 High | **Crystal Oscillator (32.768 kHz + CD4060 divider)** — Replace RC 555 with quartz crystal for ±20 ppm accuracy (~1.7 sec/day drift vs. ~3 min/day current) | Massive accuracy gain |
| 🔴 High | **RTC IC Integration (DS3231)** — Add battery-backed Real-Time Clock with I2C, maintains time through power interruptions | Commercial viability |
| 🟠 Medium | **PCB Design (KiCad / EasyEDA)** — Transfer breadboard to professional PCB; eliminates contact resistance, parasitic effects, and improves reliability | Production-ready |
| 🟠 Medium | **Alarm / Chime Functionality** — 74LS85 magnitude comparator against DIP-switch-set alarm time, driving a buzzer | Feature addition |
| 🟡 Low | **12/24-Hour Toggle Mode** — Switch with AM/PM LED indicator | User experience |
| 🟡 Low | **Multiplexed Display Drive** — Single 74LS47 + 4017 Johnson counter to time-multiplex all 6 displays at > 100 Hz | Reduces IC count |
| 🟢 Educational | **FPGA Re-implementation (Verilog/VHDL)** — Port the design to Basys 3 / DE10-Lite as a digital design bridge exercise | Modern design flow |

---

## 📁 Repository Structure

```
24-Hour-Digital-Logic-Clock/
│
├── 📄 README.md                          ← This file
│
├── 📂 docs/
│   ├── 📄 Project_Report.pdf             ← Full engineering report
│   └── 📄 Design_Notes.md               ← Additional design notes
│
├── 📂 schematics/
│   ├── 📄 full_system_schematic.pdf      ← Complete circuit schematic
│   ├── 📄 oscillator_circuit.pdf         ← 555 Timer sub-circuit
│   ├── 📄 seconds_counter.pdf            ← Seconds BCD counter pair
│   ├── 📄 minutes_counter.pdf            ← Minutes BCD counter pair
│   └── 📄 hours_counter.pdf              ← Hours BCD counter pair (Mod-24)
│
├── 📂 assets/
│   ├── 📂 images/
│   │   ├── 🖼️ breadboard_full.jpg        ← Full breadboard photo
│   │   ├── 🖼️ display_closeup.jpg        ← Display section close-up
│   │   ├── 🖼️ ic_section.jpg             ← Counter & decoder ICs
│   │   ├── 🖼️ oscillator.jpg             ← 555 Timer circuit
│   │   └── 🖼️ video_thumbnail.jpg        ← Demo video thumbnail
│   └── 📂 videos/
│       └── 🎬 clock_demo.mp4             ← Full demonstration video
│
└── 📂 datasheets/
    ├── 📄 NE555_Datasheet.pdf
    ├── 📄 74LS90_Datasheet.pdf
    ├── 📄 74LS47_Datasheet.pdf
    ├── 📄 74LS00_Datasheet.pdf
    └── 📄 74LS08_Datasheet.pdf
```

---

## 👥 Team Members

<div align="center">

<table>
<tr>
<td align="center" width="50%">

### 👨‍💻 Omar Issam Mohamed

[![GitHub](https://img.shields.io/badge/GitHub-OmarIssam-0D1B2A?style=for-the-badge&logo=github)](https://github.com/)
[![Email](https://img.shields.io/badge/Email-omar.hq.eg@gmail.com-2E6DA4?style=for-the-badge&logo=gmail&logoColor=white)](mailto:omar.hq.eg@gmail.com)
[![University](https://img.shields.io/badge/University-s--omar.halim@zewailcity.edu.eg-C9A84C?style=for-the-badge&logo=academia&logoColor=white)](mailto:s-omar.halim@zewailcity.edu.eg)

📞 +20 150 191 7900

*Circuit Design · System Architecture · Testing & Validation*

</td>
<td align="center" width="50%">

### 👨‍💻 Mahmoud Shaban Abdelkareem

[![GitHub](https://img.shields.io/badge/GitHub-MahmoudShaban-0D1B2A?style=for-the-badge&logo=github)](https://github.com/)
[![Email](https://img.shields.io/badge/Email-engmahmoud10227@gmail.com-2E6DA4?style=for-the-badge&logo=gmail&logoColor=white)](mailto:engmahmoud10227@gmail.com)
[![University](https://img.shields.io/badge/University-s--mahmoud.abdelkareem@zewailcity.edu.eg-C9A84C?style=for-the-badge&logo=academia&logoColor=white)](mailto:s-mahmoud.abdelkareem@zewailcity.edu.eg)

📞 +20 109 214 1398

*BCD Logic Design · Display Interfacing · Documentation*

</td>
</tr>
</table>

</div>

---

## 🏛️ Institution

<div align="center">

**Zewail City of Science and Technology**
Faculty of Engineering & Applied Sciences
Digital Logic Design Course — Spring Semester 2026

</div>

---

## 📝 Conclusion

This project demonstrates that a fully functional **24-hour digital clock** can be constructed from first principles using nothing more than logic gates, flip-flops, and counters — the same fundamental building blocks that underlie every modern digital system.

Key engineering outcomes:

- ✅ **Mastered** the design of non-power-of-2 modulo counters using combinational feedback
- ✅ **Applied** the complete digital design flow: specification → architecture → circuit → implementation → test
- ✅ **Validated** hardware behavior against theoretical predictions at the IC level
- ✅ **Diagnosed and resolved** real-world hardware issues: noise, timing, contact resistance, current limits
- ✅ **Built intuition** for the fundamental operation of every digital system ever designed

> *"To understand modern computing, you must first understand its atoms — gates, flip-flops, and counters. This clock is built from those atoms alone."*

---

## 📚 References

1. Texas Instruments — [SN74LS90 Decade Counter Datasheet](https://www.ti.com/lit/ds/symlink/sn74ls90.pdf)
2. Texas Instruments — [SN74LS47 BCD-to-7-Segment Decoder Datasheet](https://www.ti.com/lit/ds/symlink/sn74ls47.pdf)
3. Texas Instruments — [NE555 Precision Timer Datasheet](https://www.ti.com/lit/ds/symlink/ne555.pdf)
4. M. M. Mano & M. D. Ciletti — *Digital Design: With an Introduction to Verilog HDL, VHDL, and SystemVerilog*, 6th ed., Pearson, 2018
5. R. L. Tokheim — *Digital Electronics: Principles and Applications*, 8th ed., McGraw-Hill, 2013
6. J. F. Wakerly — *Digital Design: Principles and Practices*, 5th ed., Pearson, 2018
7. P. Horowitz & W. Hill — *The Art of Electronics*, 3rd ed., Cambridge University Press, 2015

## 📂 Project Resources

This folder contains:
- 📸 Hardware images
- 🎥 Demonstration video
- 📄 Project documentation and report

🔗 [Open Project Resources](https://drive.google.com/drive/folders/1iyDGb8mfDWPYWPMpxPGSWmzPBX2Vkbt5?usp=sharing)

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0D1B2A,1B3A5C,2E6DA4&height=100&section=footer&animation=fadeIn" alt="Footer" width="100%"/>

**⭐ If this project helped you — consider giving it a star!**

*Made with ❤️ and logic gates at Zewail City of Science and Technology*

`74LS90` · `74LS47` · `NE555` · `BCD Counter` · `7-Segment Display` · `Digital Logic` · `Breadboard`

</div>

