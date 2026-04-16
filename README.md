
# 🔧 8-bit PWM Generator (RTL to GDSII using Synopsys)

## 📌 Project Overview

This project implements a complete **RTL-to-GDSII flow** for an **8-bit Pulse Width Modulation (PWM) generator** using Synopsys EDA tools. It demonstrates the full ASIC design cycle—from RTL design to final layout—using industry-standard methodologies.

PWM is widely used in applications such as motor control, LED dimming, and power electronics. This project focuses on designing a synchronous PWM architecture and validating it through simulation, synthesis, physical design, and timing analysis.

---

## 🎯 Objectives

* Design an 8-bit PWM generator using **Verilog HDL**
* Perform functional verification using **Synopsys VCS**
* Synthesize RTL to gate-level netlist using **Design Compiler**
* Execute full physical design using **IC Compiler II**
* Perform **Static Timing Analysis (STA)** using PrimeTime
* Achieve timing closure with positive slack

---

## 🧠 Design Architecture

The PWM module consists of:

* **8-bit synchronous counter**
* **Comparator logic**

### ⚙️ Working Principle

* Counter increments every clock cycle
* Duty cycle input (8-bit) determines output pulse width
* Output logic:

  * `PWM = 1` if `counter < duty`
  * `PWM = 0` otherwise

---

## 💻 RTL Code (Verilog)

```verilog
module pwm_8bit (
    input wire clk,
    input wire rst,
    input wire [7:0] duty,
    output reg pwm_out
);

    reg [7:0] counter;

    always @(posedge clk or posedge rst) begin
        if (rst)
            counter <= 8'b0;
        else
            counter <= counter + 1'b1;
    end

    always @(posedge clk or posedge rst) begin
        if (rst)
            pwm_out <= 1'b0;
        else
            pwm_out <= (counter < duty) ? 1'b1 : 1'b0;
    end

endmodule
```

---

## 🧪 Simulation

* Tool: **Synopsys VCS**
* Testbench verifies multiple duty cycles:

  * 25%, 50%, 75%, 100%
* Waveforms generated using:

  * VCD / FSDB dumps

---

## ⚙️ Design Flow

### 1️⃣ RTL Simulation

* Functional verification using testbench
* Waveform validation

### 2️⃣ Logic Synthesis

* Tool: **Design Compiler**
* Output: Gate-level netlist
* Optimization targets:

  * Area
  * Power
  * Timing

### 3️⃣ Floorplanning

* Define core area and I/O placement
* Optimize utilization and routing feasibility

### 4️⃣ Power Planning

* Creation of:

  * Power rings
  * Power mesh
* Ensures stable VDD/VSS distribution

### 5️⃣ Placement

* Standard cell placement
* Optimized for:

  * Wirelength
  * Timing

### 6️⃣ Clock Tree Synthesis (CTS)

* Balanced clock distribution
* Reduced skew and delay

### 7️⃣ Routing

* Global + detailed routing
* DRC-clean connections
* GDSII generation

### 8️⃣ Static Timing Analysis (STA)

* Tool: **PrimeTime**
* Verified:

  * Setup timing
  * Hold timing
* Achieved **timing closure**

---

## 🏭 Technology Used

* **SAED 32nm Technology Library**
* Enables realistic ASIC implementation and timing evaluation

---

## 📊 Results

* ✅ Functional correctness verified
* ✅ Successful RTL-to-GDSII flow
* ✅ Timing constraints met (positive slack)
* ✅ Clean routed design with generated GDSII

---

## 📁 Project Structure

```
├── rtl/                # Verilog RTL code
├── tb/                 # Testbench
├── constraints/        # SDC files
├── dc/                 # Synthesis scripts & outputs
├── icc2/               # Physical design scripts
├── results/            # Netlist, SPEF, GDS
└── reports/            # Timing, area, power reports
```

---

## 🚀 Tools Used

* Synopsys VCS (Simulation)
* Synopsys Design Compiler (Synthesis)
* Synopsys IC Compiler II (Physical Design)
* Synopsys PrimeTime (STA)

---

## 📚 Key Learnings

* End-to-end ASIC design flow
* Synchronous digital design concepts
* Timing closure and constraint handling
* Industry-standard EDA tools usage

---

## 📌 Conclusion

This project successfully demonstrates the complete ASIC design flow for an 8-bit PWM generator. It bridges the gap between theoretical digital design and practical VLSI implementation using professional tools and methodologies.

---

## 👨‍💻 Author

**Anvay Pawar**

---

## ⭐ If you found this useful

Give this repo a ⭐ and feel free to fork or contribute!
