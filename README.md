# CMOS-INVERTER

CMOS Inverter Design, Schematic Capture, Layout and Simulation using Cadence Virtuoso (gpdk180)

**Objective**:

 Capture the schematic of a CMOS inverter with 0.1 pF load capacitance.
 
Simulate three different transistor width configurations:
WN = WP
WN = 2 × WP
WN = WP / 2

Perform Transient and DC Analysis.

Calculate:

High-to-Low Propagation Delay (tpHL)

Low-to-High Propagation Delay (tpLH)

Average Propagation Delay (tPD)

Design Layout and run DRC, LVS, and post-layout simulations.

**Tools & Technology**

EDA Tool: Cadence Virtuoso

Simulation Tool: Spectre via ADE L

Tech Library: gpdk180

Schematic & Layout: CMOS Inverter (VLSI Design)

**PROCEDURE**



 **STEP 1: Create a New Library**

1. Go to `Tools → Library Manager`.
2. In Library Manager, click `File → New → Library`.
3. Name your library (e.g., `VTU_LAB_MANUAL_180nm`) and click **OK**.
4. In the “Technology File” tab at the bottom, select `Attach to an existing technology library`, choose `gpdk180`, and click **OK**.

---

 **STEP 2: Create a New Cellview**

1. In Library Manager, select your library.
2. Click `File → New → Cell View`.
3. Name the cell (e.g., `CMOS_Inverter_WN_EQ_WP`), select `Tool: Schematic`, and click **OK**.

---

**STEP 3: Design the Schematic**

1. Press **‘i’** or click `Create → Instance`.
2. Add **NMOS** and **PMOS** transistors:

   * For WN = WP: W = 850n, L = 180n
   * For WN = 2WP: NMOS W = 850n, PMOS W = 1.7u
   * For WN = WP/2: NMOS W = 850n, PMOS W = 425n
3. Place input/output **pins** using ‘p’.
4. Connect them using **‘w’** for wiring.
5. Use `Check and Save`.

---

 **STEP 4: Create a Symbol**

1. Go to `Create → Cellview → From Cellview`.
2. In the window, ensure your library and cell names are correct.
3. Assign pin directions and click **OK**.
4. Use drawing tools to customize symbol (triangle and circle bubble).
5. Save the symbol (`Check and Save`).

---

 **STEP 5: Create a Testbench**

1. Create a new cellview (e.g., `CMOS_Inverter_Test`).
2. Use `Create → Instance` to add:

   * Your inverter symbol
   * `vpulse`, `vdc`, `cap`, and `gnd` from AnalogLib
3. **vpulse settings**:

   * V1 = 0 V, V2 = 1.8 V
   * Rise/Fall = 1 ps, Width = 10 ns, Period = 20 ns
4. **cap value** = 0.1 pF
5. Wire all and label nets (`L` for labels).
6. `Check and Save` the design.

---

 **STEP 6: Simulation Setup (ADE L)**

1. Open testbench → `Launch → ADE L`.
2. Setup:

   * Simulator: **Spectre**
   * Model Library: select proper `.scs` for gpdk180 and process corner
   * 
3. **DC Analysis**:

   * Sweep `vpulse` from 0 V to 1.8 V
4. **Transient Analysis**:

   * Stop time: 100 ns, Accuracy: Moderate
     
5. **Output**:

   * `Outputs → Setup → From Design`
   * Select nets: **IN**, **OUT**

---

 **STEP 7: Run Simulation**

1. Go to `Simulation → Netlist and Run`.
2. View waveforms (IN and OUT).
3. Use `Graph → Split All Strips` for better view.

---

**Calculate tpHL, tpLH, tPD**

1. Go to `Tools → Calculator` in waveform window.
2. Use intersect to find Switching Potential (where Vin = Vout).
3. Use delay function to calculate:

   * `tpLH` = delay from low to high
   * `tpHL` = delay from high to low
4. Compute: `tPD = (tpLH + tpHL) / 2`
5. Repeat for all 3 geometries.

---

**Simulation Settings**

Input Pulse:

Rise Time: 1 ps

Fall Time: 1 ps

Pulse Width: 10 ns

Period: 20 ns

Output Load Capacitance: 0.1 pF

**Results**

Transient and DC Analysis plots.

Delay parameters computed for each transistor configuration.

Best geometry for minimum delay identified.

Post-layout results compared with pre-layout simulation.

**Key Learnings**

Understanding delay behavior with different W/L ratios.

Hierarchical symbol creation in Virtuoso.

DC & transient analysis setup in ADE L.

Performing DRC, LVS, and parasitic extraction.

Use of waveform tools and calculator in Cadence.


