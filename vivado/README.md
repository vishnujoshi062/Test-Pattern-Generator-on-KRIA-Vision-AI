# Vivado part (steps 1-2)

`design_1_wrapper.xsa` is the exported **pre-synthesis** platform. It contains only the
**Zynq UltraScale+ MPSoC** (`zynq_ultra_ps_e` 3.5) with the KV260 board preset and the
unused `M_AXI_HPM*` master ports removed. DisplayPort (Dual Lower, 27 MHz ref) and PL clock 0
come from the board preset. Device: `xck26-sfvc784-2LV-c`.

The XSA was exported with **Vivado 2024.2**.

## Option A - just use the XSA
Nothing to do. Use `design_1_wrapper.xsa` in Vitis (see the main README, step 3).

## Option B - rebuild from the Tcl script
```
cd vivado
vivado -mode batch -source create_project.tcl
```
This creates `vivado/build/` (git-ignored) and writes a fresh `design_1_wrapper.xsa`.

## Option C - export Tcl from your own Vivado project
Run these in the Vivado Tcl console with your project open:

```tcl
# 1) whole project as a script
write_project_tcl -force -target_proj_dir ./build create_project.tcl

# 2) or only the block design
write_bd_tcl -force design_1.tcl
```
(GUI: *File > Project > Write Tcl...* and *File > Export > Export Block Design...*)

## Manual steps in the GUI
1. Create a project for the **Kria KV260 Vision AI Starter Kit** (select the SOM + carrier card connection).
2. Create a block design and add only **Zynq UltraScale+ MPSoC**.
3. Run Block Automation (apply board preset).
4. Disable `M_AXI_HPM0_FPD`, `M_AXI_HPM1_FPD`, `M_AXI_HPM0_LPD` (removes dangling ports).
5. *Validate Design*, then *Generate Output Products*, then *Create HDL Wrapper*.
6. *File > Export > Export Hardware*: **Pre-synthesis**, no bitstream, produces the `.xsa`.
