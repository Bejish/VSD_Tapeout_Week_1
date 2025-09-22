🚀 RISC-V SoC Tapeout Journey – Week 1, Day 1
RTL Design & Testbench Simulation Expedition








"Every waveform tells a story — and every testbench is the narrator"

🌟 Mission Control Dashboard

Objective: Understand RTL design, build a testbench, simulate with iVerilog, and visualize signals in GTKWave.
Focus: Learn the roles of Design (DUT), Stimulus Generator (Testbench), and Stimulus Observer (Waveform & Monitors).

⚙️ The Simulation Arsenal
Tool	Role	Command
⚡ iVerilog	RTL compilation & simulation	iverilog good_mux.v tb_good_mux.v -o mux_sim
📊 GTKWave	Waveform visualization	gtkwave tb_good_mux.vcd
✍️ Editor	Code authoring	nano / gedit / vim
🔄 RTL Simulation Flow
<div align="center">
graph TD
    A[📐 Design Module (DUT)] --> B[🎬 Stimulus Generator (Testbench)]
    B --> C[📝 Stimulus Observer ($monitor + VCD)]
    C --> D[⚡ iVerilog Compiler + Simulator]
    D --> E[📂 VCD Output File]
    E --> F[📊 GTKWave Waveform Viewer]
    
    style A fill:#ffcc99
    style B fill:#ccffcc
    style C fill:#ccccff
    style F fill:#ff9999

</div>

Flow Roles:

DUT → Your RTL design (e.g., good_mux.v)

Stimulus Generator → Inputs applied in TB (tb_good_mux.v)

Stimulus Observer → $dumpfile, $dumpvars, $monitor record responses

Simulator → Executes DUT + TB → Generates .vcd

Viewer → GTKWave for debugging

🧪 Lab Expedition Logs
Lab 1 – Setup Verification

✅ Cloned sky130RTLDesignAndSynthesisWorkshop repo

✅ Navigated verilog_files/

✅ Verified presence of design + testbench (good_mux.v, tb_good_mux.v)

Lab 2 – First Simulation: Good MUX
iverilog good_mux.v tb_good_mux.v -o mux_sim
./mux_sim
gtkwave tb_good_mux.vcd


📸 Waveform captured in GTKWave

When sel=0 → y=i0

When sel=1 → y=i1

Lab 3 – Testbench Anatomy

Key Elements in tb_good_mux.v:

Module declaration – no ports

Signal declarations – reg (inputs), wire (outputs)

DUT instantiation – connects TB ↔ design

Stimulus generation – input sequences

Observers – $monitor, $dumpfile, $dumpvars

initial begin
    sel = 0; i0 = 0; i1 = 0;
    #100 sel = 0; i0 = 1; i1 = 0;
    #100 sel = 1; i0 = 1; i1 = 0;
end

initial begin
    $monitor("t=%0t sel=%b i0=%b i1=%b y=%b", $time, sel, i0, i1, y);
end

Lab 4 – Design Comparison (Good vs Bad MUX)
iverilog bad_mux.v tb_bad_mux.v -o bad_mux_sim
./bad_mux_sim
gtkwave tb_bad_mux.vcd


Analysis:

Good mux → clean logic, correct behavior.

Bad mux → unintended outputs, shows why coding style matters.

📊 Key Learnings

Testbench = Stimulus + Observer

$dumpfile/$dumpvars essential for waveform logging.

$finish ensures simulation ends properly.

Comparing good vs bad design shows synthesis & functional pitfalls.

📝 Day 1 Deliverables

 Verified repo + files

 Simulated good_mux.v + TB

 Viewed waveforms in GTKWave

 Explored testbench structure

 Compared good vs bad mux design

Generated Files:

mux_sim → simulation executable

tb_good_mux.vcd → waveform database

<div align="center">
🚀 Status: Week 1 – Day 1 Completed

"Simulation mastered. Synthesis awaits!"

</div>
