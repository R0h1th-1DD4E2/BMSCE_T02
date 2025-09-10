# 🕹️ Choreo8 – Advanced LED Pattern Generator
[![GDS Build](../../workflows/gds/badge.svg)](../../actions/workflows/gds.yml)  
[![Documentation](../../workflows/docs/badge.svg)](../../actions/workflows/docs.yml)  
[![Test Suite](../../workflows/test/badge.svg)](../../actions/workflows/test.yml)  
[![FPGA Verification](../../workflows/fpga/badge.svg)](../../actions/workflows/fpga.yml)

<div align="center">

**🎯 A Simple 8-bit LED choreographer designed for Tiny Tapeout 🎯**
*Simple combinational logic for fun LED patterns and basic animation control*

</div>

---

## 🌟 Project Highlights

- **🔥 8 Mesmerizing LED Patterns** - From classic Knight Rider to pseudo-random sparkle effects
- **⚡ Dual-Speed Operation** - Intelligent clock division for 1Hz/4Hz animation rates  
- **🎛️ Real-time Control** - Pattern switching, pause/resume, and speed control
- **🧠 Smart State Management** - Pause-aware clock dividers and pattern state preservation
- **🔬 Comprehensive Verification** - 100+ test cycles with Cocotb Python testbench
- **🏭 Production-Ready** - Synthesizable for both ASIC (Tiny Tapeout) and FPGA platforms

---

## 📖 Technical Overview
**Choreo8** is an 8-bit LED pattern generator designed for Tiny Tapeout. It implements multiple LED animation effects using efficient state machines and simple digital logic, demonstrating practical sequential circuit design for ASIC and FPGA platforms.

### 🏗️ Core Architecture

```
    5MHz Clock Input
           ↓
    ┌─────────────────┐
    │  Clock Divider  │ ← speed_sel, pause
    │                 │
    └─────────────────┘
           ↓
    1Hz/4Hz Derived Clock
           ↓
    ┌─────────────────┐
    │ Pattern Select  │ ← ena, pat_sel[2:0]
    │         Logic   │
    └─────────────────┘
           ↓
    ┌─────────────────┐
    │ Pattern Engine  │ ← Internal state registers
    │  (8 Algorithms) │   (LFSR, counters, FSMs)
    └─────────────────┘
           ↓
      led_out[7:0]
```

---

## ✨ Pattern Showcase

| Pattern | Algorithm | State Elements | Visual Description |
|---------|-----------|----------------|-------------------|
| **🏎️ Knight Rider** | Bidirectional FSM | `knight_pos[1:0]`, `knight_dir` | Symmetric LEDs sweep back and forth like KITT |
| **🚶 Walking Pair** | Linear traversal | `walk_pos[2:0]`, `walk_dir` | Two adjacent LEDs march left and right |
| **🔄 Expand/Contract** | Cyclical pattern | `expand_pose[2:0]` | LEDs grow from center, then contract |
| **💫 Blink All** | Toggle generator | `toggle_state` | Synchronized full-array blinking |
| **♟️ Alternate** | Checkerboard toggle | `toggle_state` | Classic odd/even LED alternation |
| **🎪 Marquee** | Barrel shifter | `marquee_reg[7:0]` | Theater-style rotating chase lights |
| **✨ Random Sparkle** | 8-bit LFSR | `lfsr[7:0]` | Pseudo-random flicker (maximal sequence) |
| **🌙 All Off** | Static output | - | Complete LED array disable |


---

### Tiny Tapeout Pin Assignment
| TT Pin | Signal | Direction | Function |
|--------|--------|-----------|----------|
| `clk` | System Clock | Input | 5MHz reference clock |
| `rst_n` | Reset | Input | Active-low asynchronous reset |
| `ui_in[5]` | Module Enable | Input | Pattern update gate |
| `ui_in[4]` | Pause Control | Input | Freeze current state |
| `ui_in[3]` | Speed Select | Input | `0`=4Hz, `1`=1Hz |
| `ui_in[2:0]` | Pattern Select | Input | 3-bit pattern code |
| `uo_out[7:0]` | LED Output | Output | Direct LED drive signals |

---


### 🎮 Real-time Control Features
- **Pattern Switching**: Change `ui_in[2:0]` while `ui_in[5]` is high
- **Speed Control**: Toggle `ui_in[3]` for 4× speed difference  
- **Pause/Resume**: Use `ui_in[4]` to freeze/unfreeze current state
- **Emergency Stop**: Assert reset for immediate all-off state

---

## 🧪 Verification & Testing

### 🐍 Cocotb Test Framework
The project features a **comprehensive Python-based testbench** using Cocotb


### 📊 Test Coverage Matrix
| Test Category | Test Cases | Verification Points |
|---------------|------------|-------------------|
| **Pattern Generation** | 8 patterns × 2 speeds | State transitions, output correctness |
| **Control Logic** | Enable/disable, pause/resume | Signal gating, state preservation |
| **Reset Behavior** | Async reset | Initial conditions, state clearing |
| **Timing Control** | Clock division, speed switching | Frequency accuracy, glitch-free |
| **Pattern Switching** | Dynamic pattern changes | State machine integrity |



### 🔬 Advanced Test Features
- **Real-time Pattern Monitoring**: Cycle-by-cycle LED state logging
- **Pause State Verification**: Ensures frozen patterns maintain exact state
- **Pattern Switching Validation**: Confirms clean transitions between modes  
- **Clock Domain Testing**: Verifies correct frequency division
- **Reset Recovery Testing**: Validates proper initialization sequences

---



### 🔧 Design Optimizations
- **Clock Domain Separation**: Isolated pattern logic from system clock
- **State Preservation**: Pause functionality maintains exact pattern position  
- **Resource Sharing**: Efficient toggle_state usage across multiple patterns
- **Reset Strategy**: Asynchronous reset with synchronous release
- **Pattern Memory**: Optimized state encoding for minimal register usage

---


## 🎨 Applications & Extensions

### 🎪 Demonstration Uses
- **Digital Design Education**: State machines, timing, sequential logic
- **LED Art Installations**: Programmable light shows and displays
- **Embedded System Projects**: Real-time control and pattern generation
- **FPGA Learning Platform**: Hands-on hardware programming


---

## 🏆 Technical Achievements

### 🎯 Design Excellence
- **Zero-Glitch Pattern Switching**: Clean transitions between all 8 patterns
- **Pause-Aware Clock Management**: Maintains timing integrity during freeze states
- **Robust Reset Architecture**: Guaranteed initialization in all operating conditions
- **Efficient State Encoding**: Minimal register usage with maximum functionality

### 🧠 Advanced Algorithms  
- **Maximal-Length LFSR**: 255-cycle pseudo-random sequence for sparkle effect
- **Bidirectional State Machines**: Smooth direction reversals in motion patterns  
- **Symmetric Pattern Generation**: Mathematical LED positioning algorithms
- **Real-time Speed Control**: Glitch-free frequency switching

---


## 📜 License & Acknowledgments

**License**: Apache 2.0 - See [LICENSE](LICENSE) file for details

## Special Thanks 

- **Dr.Camilo Vélez Cuervo** , *IEEE Electron Devices Society (EDS)*
- **Prof. Dr. R. Jaya Gowri**, *BMS College of Engineering*
- **Matt Venn** , *Tiny Tapeout*
- **G S Bharath** , *Instructor*
 


---




</div>
