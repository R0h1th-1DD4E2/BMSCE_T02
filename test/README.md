# Testing Framework Documentation

This repository contains a comprehensive testing framework for the LED Pattern Generator project using CocoTB (Coroutine Co-simulation TestBench) and Icarus Verilog simulator.

## File Structure

```
test/
├── requirements.txt    # Python dependencies
├── Makefile           # Build and simulation configuration
├── tb.v               # Verilog testbench wrapper
├── tb.gtkw            # GTKWave waveform viewer configuration
└── test.py            # Main Python test suite
```

## File Descriptions

### requirements.txt
Contains Python package dependencies:
- `pytest==8.3.4` - Testing framework
- `cocotb==1.9.2` - Coroutine-based co-simulation testbench framework

### Makefile
Build configuration file that:
- Sets up Icarus Verilog as the default simulator
- Configures source file paths from `../src/` directory
- Supports both RTL and gate-level simulation
- Handles include paths and compilation arguments
- Integrates with CocoTB framework

### tb.v (Testbench Wrapper)
Verilog module that:
- Instantiates the `tt_um_BMSCE_T2` design under test
- Creates VCD dump file for waveform analysis
- Defines all input/output signals as registers/wires
- Handles power pins for gate-level testing
- Maps signals to the LED pattern generator module

### tb.gtkw
GTKWave configuration file that:
- Defines waveform viewer layout and settings
- Specifies which signals to display
- Groups signals logically (Inputs, Bidirectional Pins, Output Pins)
- Sets up time scale and display preferences

### test.py
Main Python test suite containing:
- `LEDPatternTester` class with comprehensive testing methods
- Two test functions: detailed and basic functionality tests
- Pattern testing for all 8 LED patterns
- Speed control testing (fast/slow)
- Pause functionality verification
- Reset behavior validation
- Enable signal testing

## Usage Instructions

### Prerequisites
1. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Ensure Icarus Verilog is installed:
   ```bash
   # Ubuntu/Debian
   sudo apt-get install iverilog
   
   # macOS with Homebrew
   brew install icarus-verilog
   ```

### Running Tests

#### RTL Simulation (Default)
```bash
make
```
This runs the full test suite against the RTL source files.

#### Basic Test Only
```bash
make MODULE=test::test_basic_functionality
```
Runs only the simplified basic functionality test.

#### Gate Level Simulation
```bash
make GATES=yes
```
Runs tests against the synthesized gate-level netlist (requires PDK setup).

#### Clean Build Files
```bash
make clean
```

### Test Output
Tests generate several output files:
- `tb.vcd` - Waveform dump file for signal analysis
- `sim_build/` - Simulation build directory with logs
- Console output with detailed test results and pattern analysis

## Test Coverage

### Pattern Tests
The test suite validates all 8 LED patterns:
1. **Knight Rider** - Scanning LED effect
2. **Walking Pair** - Two adjacent LEDs moving
3. **Expand/Contract** - LEDs expanding from center and contracting
4. **Blink All** - All LEDs blinking simultaneously
5. **Alternate** - Alternating LED pattern
6. **Marquee** - Rotating LED chase pattern
7. **Random Sparkle** - Random LED activation
8. **All Off** - All LEDs disabled

### Feature Tests
- **Speed Control**: Tests both fast (8Hz) and slow (2Hz) speeds
- **Pause Functionality**: Verifies pattern freezing/resuming
- **Reset Behavior**: Ensures proper reset to initial state
- **Enable Control**: Tests ui_in[5] enable functionality
- **Pattern Switching**: Validates dynamic pattern changes

### Signal Mapping
The tests use the following signal mapping:
- `ui_in[2:0]` - Pattern selection (3 bits = 8 patterns)
- `ui_in[3]` - Speed control (0=fast, 1=slow)
- `ui_in[4]` - Pause control (0=run, 1=pause)
- `ui_in[5]` - Enable signal for pattern changes
- `uo_out[7:0]` - 8-bit LED output

## Waveform Analysis

To view simulation waveforms:
1. Run tests to generate `tb.vcd`
2. Open with GTKWave:
   ```bash
   gtkwave tb.vcd tb.gtkw
   ```
3. The `.gtkw` file automatically loads the signal configuration

## Customization

### Adding New Tests
1. Create new test functions in `test.py` decorated with `@cocotb.test()`
2. Use the `LEDPatternTester` class methods for consistent testing
3. Follow the existing pattern for clock management and signal setup

### Modifying Patterns
1. Update the `pattern_names` dictionary in `LEDPatternTester`
2. Adjust test cycles and expected behaviors in pattern-specific tests
3. Update signal mapping if hardware interface changes

### Simulation Parameters
- Clock period: 125ms (8Hz) for pattern visibility
- Reset duration: 2 clock cycles
- Pattern observation: Variable cycles based on pattern complexity
