# Day 1 - Week 1: Introduction to Verilog RTL Design and Testbench

## 🎯 Learning Objectives
- Understand the RTL design flow and simulation methodology
- Learn the structure and components of Verilog testbenches
- Master iVerilog compilation and GTKWave waveform analysis
- Implement and verify basic digital design modules

## 📋 Prerequisites
- Basic knowledge of digital logic design
- Understanding of Verilog HDL syntax
- Linux terminal familiarity

## 🛠️ Tools Required
- **iVerilog**: Verilog compiler and simulator
- **GTKWave**: Waveform viewer
- **Text Editor**: nano/vim/gedit for code editing

## 🔄 Simulation Flow Overview

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Design    │    │ Testbench   │    │  iVerilog   │
│   Module    │───▶│  (TB)       │───▶│  Compiler   │
│   (.v)      │    │   (.v)      │    │             │
└─────────────┘    └─────────────┘    └─────────────┘
                                             │
                                             ▼
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  GTKWave    │◀───│  VCD File   │◀───│ Simulation  │
│  Viewer     │    │ (.vcd)      │    │ Executable  │
└─────────────┘    └─────────────┘    └─────────────┘
```

## 📁 Directory Structure
```
sky130RTLDesignAndSynthesisWorkshop/
├── verilog_files/
│   ├── good_mux.v          # 2:1 Multiplexer design
│   ├── tb_good_mux.v       # Testbench for good_mux
│   ├── bad_mux.v           # Faulty mux (learning example)
│   ├── bad_case.v          # Case statement examples
│   └── [other design files...]
├── my_lib/
│   ├── lib/                # Liberty files
│   └── verilog_model/      # Standard cell models
└── README.md
```

## 🧪 Lab Activities

### **Lab 1: Environment Setup and Tool Verification**

#### Step 1: Navigate to Working Directory
```bash
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
ls -la
```

#### Step 2: Examine Design Files
```bash
# View the good_mux design
cat good_mux.v

# View the corresponding testbench
cat tb_good_mux.v
```

#### Step 3: Understanding Testbench Structure
A testbench typically contains:
- **Module Declaration** (no ports)
- **Signal Declarations** (reg for inputs, wire for outputs)
- **Design Instantiation** (DUT - Device Under Test)
- **Stimulus Generation** (input patterns)
- **Response Monitoring** (output verification)
- **Simulation Control** (`$dumpfile`, `$dumpvars`, `$finish`)

### **Lab 2: First Simulation - Good Multiplexer**

#### Step 1: Compile the Design
```bash
iverilog good_mux.v tb_good_mux.v -o mux_sim
```

#### Step 2: Execute Simulation
```bash
./mux_sim
```
**Expected Output:**
- VCD file generation message
- Simulation completion without errors

#### Step 3: View Waveforms
```bash
gtkwave tb_good_mux.vcd
```

#### Step 4: Waveform Analysis
In GTKWave:
1. **Add Signals**: Drag signals from signal list to waveform window
2. **Analyze Behavior**: 
   - When `sel = 0`: `y = i0`
   - When `sel = 1`: `y = i1`
3. **Verify Timing**: Check setup and hold times
4. **Save Session**: File → Write Save File

### **Lab 3: Testbench Components Deep Dive**

#### Understanding Key Testbench Elements

**1. Clock Generation:**
```verilog
initial begin
    clk = 0;
    forever #10 clk = ~clk;  // 20ns period clock
end
```

**2. Stimulus Application:**
```verilog
initial begin
    // Initialize inputs
    sel = 0; i0 = 0; i1 = 0;
    
    // Apply test vectors
    #100 sel = 0; i0 = 1; i1 = 0;
    #100 sel = 1; i0 = 1; i1 = 0;
    // ... more test cases
end
```

**3. Response Monitoring:**
```verilog
initial begin
    $monitor("Time=%0t sel=%b i0=%b i1=%b y=%b", 
             $time, sel, i0, i1, y);
end
```

### **Lab 4: Design Analysis Exercise**

#### Compare Good vs Bad Design
```bash
# Simulate bad_mux for comparison
iverilog bad_mux.v tb_bad_mux.v -o bad_mux_sim
./bad_mux_sim
gtkwave tb_bad_mux.vcd
```

#### Analysis Questions:
1. What makes a design "good" vs "bad"?
2. How do you identify timing violations?
3. What are the synthesis implications?

## 📊 Key Concepts Covered

### **1. RTL Design Methodology**
- **Behavioral vs Structural modeling**
- **Synthesis considerations**
- **Design for testability**

### **2. Testbench Best Practices**
- **Complete input coverage**
- **Edge case testing**
- **Self-checking testbenches**
- **Proper simulation control**

### **3. Simulation Debug Techniques**
- **Waveform analysis**
- **Text-based monitoring**
- **Hierarchical signal viewing**

## 🔍 Common Issues and Solutions

| Issue | Symptom | Solution |
|-------|---------|----------|
| Compilation Error | `iverilog` fails | Check syntax, file paths |
| No Waveform | Empty GTKWave | Verify `$dumpfile` and `$dumpvars` |
| Simulation Hangs | No `$finish` | Add proper simulation termination |
| Wrong Results | Incorrect output | Review stimulus timing and logic |

## 📝 Lab Report Template

### **Simulation Results:**
1. **Design Analyzed:** [Design Name]
2. **Functionality Verified:** [Pass/Fail]
3. **Key Observations:**
   - Input/Output relationship
   - Timing behavior
   - Any anomalies found

### **Waveform Screenshots:**
- Include labeled waveforms showing key functionality

### **Code Analysis:**
- Design code structure
- Testbench methodology
- Synthesis implications

## 🎯 Day 1 Deliverables

### **Completed Tasks Checklist:**
- [ ] Environment setup verified
- [ ] good_mux simulation completed
- [ ] Waveforms analyzed in GTKWave
- [ ] Testbench structure understood
- [ ] Bad design comparison performed
- [ ] Lab report documentation

### **Files Generated:**
- `mux_sim` (simulation executable)
- `tb_good_mux.vcd` (waveform database)
- GTKWave save file
- Lab report documentation

## 🚀 Preparation for Day 2
- Review synthesis concepts
- Understand library formats
- Prepare for hierarchical designs
- Study standard cell libraries

---

## 📚 Additional Resources
- [Verilog HDL Reference](http://www.verilog.com)
- [iVerilog Documentation](http://iverilog.icarus.com)
- [GTKWave User Manual](http://gtkwave.sourceforge.net)

## 🤝 Support
For issues or questions:
1. Check simulation log files
2. Verify file permissions and paths
3. Review Verilog syntax carefully
4. Consult tool documentation

**Happy Learning! 🎉**

*Remember: Good simulation methodology is the foundation of successful RTL design!*
