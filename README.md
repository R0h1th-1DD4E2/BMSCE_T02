# 🕹️ Choreo8 – LED Pattern Generator  

[![](../../workflows/gds/badge.svg)](../../actions/workflows/gds.yml)  
[![](../../workflows/docs/badge.svg)](../../actions/workflows/docs.yml)  
[![](../../workflows/test/badge.svg)](../../actions/workflows/test.yml)  
[![](../../workflows/fpga/badge.svg)](../../actions/workflows/fpga.yml)  

---

## 📖 Overview  
**Choreo8** is an **8-bit LED pattern generator** designed for **[Tiny Tapeout](https://tinytapeout.com/)**.  
It demonstrates sequential digital design concepts including **state machines, pattern generation, speed control, clock division, and pause/resume functionality**.  

The project can be synthesized for **ASIC** (Tiny Tapeout flow) or tested on **FPGA boards** with LED outputs.  

---

## ✨ Features  
- **8 Built-in LED Patterns**:  

| Code | Pattern Name            | Description |
|------|-------------------------|-------------|
| `000` | Knight Rider           | Symmetric LEDs sweeping back and forth |
| `001` | Walking Pair           | Two adjacent LEDs moving left/right |
| `010` | Expanding/Contracting  | LEDs grow/shrink around center |
| `011` | Blink All              | All LEDs toggle ON/OFF |
| `100` | Alternate              | Checkerboard style toggle |
| `101` | Marquee                | Rotating "chaser" lights |
| `110` | Random Sparkle         | LFSR-based random flicker |
| `111` | All Off                | Disable LEDs |

- **Controls**:  
  - `ui_in[2:0]` → Pattern select  
  - `ui_in[3]` → Speed select (`0 = fast`, `1 = slow`)  
  - `ui_in[4]` → Pause/Resume  
  - `ui_in[5]` → Enable  

- **Outputs**:  
  - `uo_out[7:0]` → LED drive signals  

- **Clock Divider**:  
  - Designed for an **8 Hz reference clock**  
  - Provides **1 Hz (slow)** and **4 Hz (fast)** animation speeds  

---

## 🔌 Pinout  

| Signal        | Direction | Width | Description                       |
|---------------|-----------|-------|-----------------------------------|
| `clk`         | Input     | 1     | System clock (~8 Hz expected)     |
| `rst_n`       | Input     | 1     | Active-low reset                  |
| `ui_in[2:0]`  | Input     | 3     | Pattern select                    |
| `ui_in[3]`    | Input     | 1     | Speed select                      |
| `ui_in[4]`    | Input     | 1     | Pause control                     |
| `ui_in[5]`    | Input     | 1     | Enable                            |
| `uo_out[7:0]` | Output    | 8     | LED pattern output                |
| `uio_*`       | –         | –     | Not used                          |

---

## ▶️ Usage  

1. Assert **reset** (`rst_n = 0 → 1`) to initialize.  
2. Set **Enable** (`ui_in[5] = 1`).  
3. Choose pattern using `ui_in[2:0]`.  
4. Adjust speed via `ui_in[3]`.  
5. Pause/resume pattern with `ui_in[4]`.

  
---

## 🧪 Verification  

- **Testbench**: Written in **[Cocotb](https://www.cocotb.org/)** (Python-based verification).  
- Simulators supported: **ModelSim/Questa**, **Icarus Verilog**, **Verilator**.  
- Test coverage:  
  - Reset functionality  
  - Enable gating  
  - Pause/resume behavior  
  - Pattern generation (all 8 modes, fast + slow)  
  - Pattern switching correctness
    
---

## 🙏 Credits & Acknowledgments  

This project is carried out with the support and guidance of:  

- **Prof. Dr. Jaya Gowri**, *BMS College of Engineering*  
- **IEEE Electron Devices Society (EDS)**  
- **Tiny Tapeout Community**  
