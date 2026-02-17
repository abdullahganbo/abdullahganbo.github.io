# TPS5430 Non-Isolated Buck Converter (5.5–36 V → 5 V)

## Objective
Design a reference-grade, non-isolated DC-DC buck converter based on **TPS5430**, focusing on correct power-stage design, datasheet-driven component selection, and disciplined **2-layer PCB** layout execution. The goal is correctness, manufacturability, and honest derating rather than feature breadth.

---

## System Overview
- Controller: **TPS5430DDAR** (integrated high-side MOSFET)
- Topology: Non-isolated buck
- Input: **5.5–36 V DC**
- Output: **5 V regulated**
- Output current: up to **3 A peak**, realistic **~2–2.5 A continuous** (thermally limited)
- PCB: **2-layer**, **Layer 2 solid GND plane**
- Testability: test points for **VIN**, **PH**, **VOUT**, and **GND**

---

## Key Design Decisions
- External **Schottky catch diode** used to improve efficiency and reduce loss in the freewheel path.
- **22 µH inductor** selected to balance ripple current and saturation margin across a wide VIN range.
- **Polymer output capacitor** used to reduce ripple (ESR contribution) and improve transient response.
- **Enable tied to VIN** for simple, predictable startup.
- Layout is designed around **short high-di/dt loops**, controlled **PH copper**, and a **continuous ground reference**.

---

## Schematic and Layout Reference

<div style="display: flex; gap: 16px; align-items: flex-start;">
  <img src="../assets/tps5430-buck/schematic.png" width="48%" alt="TPS5430 schematic">
  <img src="../assets/tps5430-buck/top_layer.png" width="48%" alt="Top layer layout">
</div>

<div style="text-align:center; font-size: 0.95em; margin-top: 6px;">
  <a href="../assets/tps5430-buck/schematic.pdf" target="_blank">View full schematic (PDF)</a>
</div>

---

## Power Stage Architecture
The TPS5430 internal high-side MOSFET drives the **PH (switch node)** into the inductor, with a Schottky diode providing the freewheel path. The power flow is intentionally easy to verify on the PCB:
**VIN → PH → L → VOUT**.

---

## Input Network and Hot Loop Control
Input capacitors are placed close to the VIN/GND pins to support pulsed switching currents and reduce input loop area. The **high-di/dt hot loop** (MOSFET → diode → input caps) is kept compact to reduce ringing and radiated noise.

---

## Switch Node (PH) Strategy
The PH copper is kept tight and localized. This reduces capacitive coupling into the ground plane and minimizes unintended antenna behavior. Test access to **PH** is provided via a dedicated test point for safe probing during bring-up.

---

## Feedback and Regulation
The feedback divider is placed close to the IC and routed away from the PH region to reduce noise injection. The sensing path is kept short and referenced to a clean ground return.

---

## Grounding Strategy (Layer 2 Plane)
Layer 2 is used as a **continuous ground plane** to provide a low-impedance return path and reduce loop area for power switching currents. Ground stitching and direct returns are used to keep the power stage stable and predictable on a 2-layer stack-up.

<div style="display: flex; gap: 16px; align-items: flex-start; margin-top: 10px;">
  <img src="../assets/tps5430-buck/all_layers.png" width="70%" alt="All layers view with GND plane">
</div>

---

## Thermal Considerations and Derating
Thermal vias are used to spread heat into the copper and ground plane. The design assumes **thermal limits dominate** before electrical limits on a compact 2-layer PCB, so the continuous current rating is stated conservatively (**~2–2.5 A**) even though the controller supports higher peak current.

---

## Testability and Bring-Up
Dedicated test points:
- **VIN** (input)
- **PH** (switch node)
- **VOUT** (regulated output)
- **GND**

This supports controlled probing and debugging without disturbing critical current paths.

---

## Issues, Limitations, and Rev B Notes
- EMI/noise has not been measured yet (scope validation pending).
- Sustained full-load thermal performance has not been characterized.
- Future improvements may include an optional **snubber footprint** and minor hot-loop tightening if manufacturability allows.

---

## Status
- Schematic complete
- Layout complete
- DRC/ERC clean
- Fabrication pending
