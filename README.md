# Rectifier Lab · Interactive Power Electronics Simulator

Developed by **Sahil** (Roll No: **24EE10085**), Department of Electrical Engineering.

A high-fidelity, interactive power electronics simulator for single-phase and three-phase uncontrolled and phase-controlled rectifiers with resistive (R) and inductive (RL) loads.

---

## ⚡ Supported Circuits & Topologies

| Circuit Topology | Device Control | Single-Phase (1-Phase) | Three-Phase (3-Phase) |
|---|---|:---:|:---:|
| **Half-Wave** | Uncontrolled (Diode) | ✓ (1-pulse, $V_{dc} = V_m/\pi$) | ✓ (3-pulse star, $V_{dc0} = \frac{3\sqrt{3}}{2\pi}V_m$) |
| **Half-Wave** | Controlled (Thyristor / SCR) | ✓ (Firing angle $\alpha$, with/without FWD) | ✓ (Firing angle $\alpha$, 3-pulse) |
| **Full-Wave Centre-Tap** | Uncontrolled (Diode) | ✓ (2-pulse, PIV = $2V_m$) | — *(Single-phase transformer)* |
| **Full-Wave Centre-Tap** | Controlled (Thyristor / SCR) | ✓ (2-pulse, PIV = $2V_m$) | — *(Single-phase transformer)* |
| **Bridge** | Uncontrolled (Diode) | ✓ (2-pulse, PIV = $V_m$) | ✓ (6-pulse, PIV = $\sqrt{3}V_m$) |
| **Bridge** | Half-Controlled (Semi-Converter) | ✓ Symmetrical (T1, T3 / D4, D2)<br>✓ Asymmetrical (T1, T2 / D1, D2) | ✓ Common-Cathode SCRs (T1, T3, T5)<br>✓ Common-Anode SCRs (T4, T6, T2) |
| **Bridge** | Fully Controlled (Full Converter) | ✓ (4 SCRs, inversion capable) | ✓ (6 SCRs, 6-pulse sequence) |

---

## 🔬 Core Physics & Waveform Synchronization

1. **Exact Dynamic Simulation Model:**
   - Discretized at $0.25^\circ$ ($1440$ steps/cycle, $2880$ steps for two full cycles) with exact analytical exponential decay $\exp(-R\cdot \Delta t / L)$ for the inductive current.
   - Natural commutation boundaries computed accurately for single- and three-phase systems ($30^\circ$, $60^\circ$, $120^\circ$, $180^\circ$).
   - Handles continuous (CCM) and discontinuous (DCM) conduction modes without numerical instability.
   - Accurately models free-wheeling diode action and bridge inherent freewheeling.

2. **Synchronized 4-Panel Laboratory Oscilloscope:**
   - **Panel 1 (Supply Voltages):** AC source waveform ($v_s$ for 1-phase; $v_1, v_2$ for centre-tap; $v_a, v_b, v_c$ for 3-phase).
   - **Panel 2 (Rectified Output Voltage $v_o$):** Output voltage waveform, ghost candidate voltage envelopes, average $V_{dc}$ dashed reference, and gate trigger indicators ($\alpha$ arrows with SCR labels).
   - **Panel 3 (Currents):** Load current $i_o$ (amber) and source/phase current $i_a$ (indigo/cyan).
   - **Panel 4 (Device Voltage):** Anode-to-cathode voltage across reference device ($v_{D1}$ or $v_{T1}$) with Peak Inverse Voltage (PIV) limit reference line.

3. **Active Interactive Schematic Diagram:**
   - Animated vector circuit diagram highlighting currently conducting devices in real time.
   - Thyristors pulse brightly when receiving gate trigger pulses.
   - Animated dashed current flow loops follow the active closed circuit path, including freewheeling loops.

4. **Digital Cursor Probe (Laboratory Instrument):**
   - Real-time readout of phase angle $\omega t$ (degrees and radians), time $t$, conducting device list, instantaneous $v_s$, $v_o$, $i_o$, $v_{dev}$, and load power $p_o(t)$.

5. **Engineering Metrics & Performance Analysis:**
   - Average DC voltage $V_{dc}$ and current $I_{dc}$
   - RMS voltage $V_{rms}$ and current $I_{rms}$
   - Form Factor ($FF = V_{rms} / V_{dc}$)
   - Voltage Ripple Factor ($RF = \sqrt{FF^2 - 1}$)
   - Ripple Frequency ($p \times f$) and Peak-to-Peak ripple ($V_{pp}$)
   - Peak Inverse Voltage (PIV)
   - Conduction angle $\gamma$ per cycle
   - Conduction mode badge (Continuous CCM vs Discontinuous DCM)
   - Exact theoretical formula verification and comparison
   - Load time constant $\tau = L/R$ and electrical angle ratio $\omega L / R$

---

## 🎨 Interface & UX Enhancements

- **Modern Theme System:** Full Dark and Light theme support with automatic system preference detection and manual toggle.
- **Quick Operating Presets:** Instant configuration of classic benchmark modes:
  - Pure Resistive Load ($L = 0$)
  - Highly Inductive Load ($L = 100\text{ mH}$, continuous CCM)
  - Controlled Firing $\alpha = 30^\circ$
  - Controlled Firing $\alpha = 60^\circ$ (boundary of discontinuous conduction)
  - Firing $\alpha = 90^\circ$ (inversion limit)
  - Freewheeling Diode (FWD) clamping demonstration
- **Interactive Oscilloscope Scrubbing:** Click and drag anywhere across the waveforms to inspect instantaneous operating values, with keyboard arrow keys and spacebar play/pause support.
- **Mobile Responsive:** Fluid layout that adapts across desktop displays, tablets, and smartphones.

---

## 🚀 Running Locally

No installation or build step required. Open `index.html` in any modern web browser or start a local server:

```bash
# Python 3
python3 -m http.server 8000
```
Then visit `http://localhost:8000`.
