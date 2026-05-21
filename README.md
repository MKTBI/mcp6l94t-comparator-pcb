# 🔌 MCP6L94T Analog Comparator Board — BSc PCB Design

> A 4-channel voltage threshold detector built around the MCP6L94T quad op-amp,
> fully designed in KiCad from schematic to 3D render.

📄 BSc Mechatronics Engineering · 2020

---

## 📌 Project Overview

This was my first complete PCB design. The goal was to design a functional analog comparator circuit using the MCP6L94T op-amp, route it on a real PCB, and produce a manufacturable board file , handling the full workflow from schematic capture to Gerber export and 3D verification.

The circuit uses four comparator channels to drive individual LEDs, powered by a 9V battery with a push-to-test function for manual verification.

---

## ⚙️ Circuit Overview

| Property | Value |
|---|---|
| Core IC | MCP6L94T-E/SL — Quad Op-Amp (SOP-14) |
| Supply | 9V DC battery (BT1) |
| Voltage ladder | R2 (3.3kΩ) + R3–R6 (4× 10kΩ) — sets four inverting thresholds |
| Input reference | D5 (6V Zener) + R1 (10kΩ) + R11 (1MΩ) — stable ~6V on VIN+ |
| Input clamping | D3 (6V Zener) + R2 (3.3kΩ) |
| Outputs | 4× LED indicators with 3.3kΩ current limiters (R7–R10) |
| Bypass capacitor | 0.1µF (C1) on VDD |
| Reverse polarity | D2 diode protection |
| Test function | Push-to-test button — forces all LEDs ON simultaneously |
| EDA Tool | KiCad 5.1.5 |

---

## 💡 How It Works

The circuit is a **4-channel voltage threshold detector** built around the MCP6L94T quad op-amp in open-loop comparator configuration.

**Resistor ladder (VIN− inputs):**
- R2–R6 form a voltage divider from 9V to GND
- Each ladder tap connects to one VIN− (inverting input):
  - Pin 2 VINA− → tap between R2 and R3
  - Pin 6 VINB− → tap between R3 and R4
  - Pin 9 VINC− → tap between R4 and R5
  - Pin 13 VIND− → tap between R5 and R6
- This creates four decreasing reference thresholds on the inverting inputs

**Reference signal (VIN+ inputs):**
- D5 (6V Zener) + R1 (10kΩ) + R11 (1MΩ) set a stable ~6V signal
- This fixed voltage feeds the non-inverting VIN+ inputs of the comparators

**Comparator logic:**
- Each channel compares the fixed ~6V input against its ladder threshold
- If VIN+ > VIN− → output HIGH → LED lights up
- If VIN+ < VIN− → output LOW → LED stays off
- LEDs activate based on which thresholds the input voltage crosses

**Push-to-test:**
- Connects 9V directly to all outputs simultaneously
- All 4 LEDs light up — confirms all LEDs and output paths are functional

---

## 🖼 Board Preview

### Front Side (F.Cu)
![PCB Front](renders/pcb_front.png)

### Back Side (B.Cu)
![PCB Back](renders/pcb_back.png)

### 3D Render — Front
![3D Front](renders/3d_front.png)

### 3D Render — Back
![3D Back](renders/3d_back.png)

---

## 🛠 Design Workflow

1. **Schematic capture** — all components placed and connected in KiCad Schematic Editor
2. **PCB layout** — manual trace routing, component placement optimized for signal flow
3. **Gerber export** — full layer set exported for fabrication readiness
4. **Drill file export** — PTH and NPTH drill files generated
5. **3D render** — front and back verification before finalization
6. **Design review** — identified and corrected placement issues caught only in 3D view

---

## 📁 Repository Structure

```
mcp6l94t-comparator-pcb/
│
├── schematic/
│   ├── schematic.sch           
│   └── schematic.pdf      
│
├── pcb/
│   └── board.kicad_pcb
│
├── gerbers/
│   ├── F_Cu.gbr
│   ├── B_Cu.gbr
│   ├── F_Mask.gbr
│   ├── B_Mask.gbr
│   ├── F_Paste.gbr
│   ├── B_Paste.gbr
│   ├── F_SilkS.gbr
│   ├── B_SilkS.gbr
│   ├── Edge_Cuts.gbr
│   ├── PTH.drl
│   └── NPTH.drl
│
├── renders/
│   ├── pcb_front.png
│   ├── pcb_back.png
│   ├── 3d_front.png
│   └── 3d_back.png
│
├── mcp6l94t-comparator-pcb.pro
└── README.md
```

---

## 🔑 Key Learnings

- **3D rendering is not optional** — caught placement conflicts completely invisible in 2D layout
- **Ground planes matter** — routing without a solid copper fill creates unnecessary noise risk; first thing I'd fix in a redesign
- **SMD footprint sizing** — learned to balance component size against manual solderability

---

## 🔮 What I'd Do Differently Today

- Add a copper fill ground plane on both layers
- Tighten trace routing around the IC — reduce stub lengths
- Add test points on each comparator output for easier probing
- Use a regulated 5V supply instead of raw 9V battery

---

## 👤 Author

**Seyed Danial Maktabi**
BSc Mechatronics Engineering | MSc Data Analytics

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://www.linkedin.com/in/danial-maktabi-79aab118a/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-black)](https://github.com/danial-maktabi)

---

## 📄 License

Open hardware — feel free to reference or adapt with attribution.