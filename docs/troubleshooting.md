# Troubleshooting

| Symptom | Likely cause / fix |
|---------|--------------------|
| Monitor stays **black**, no error | `m` (math) library missing in `UserConfig.cmake`. Add `"m"` under *Linker Settings > Libraries*. |
| Nothing runs / PMU errors | `psu_pmu_0` ELF (`pmufw.elf`) missing in `launch.json`, or listed **after** the A53 core. PMU must be **first**, A53 second. |
| Board not initialised, PL has no clock | *Board Initialization* still set to **FSBL**. Switch it to **TCL** (runs `psu_init.tcl`). |
| `pmufw.elf` not found | Path is `<workspace>/platform_ps/export/platform_ps/sw/standalone_psu_cortexa53_0/qemu/pmufw.elf`. Build the platform first. |
| Bitstream file not found when launching | Check the *Bitstream File* path in `launch.json`; it is created in the app's `_ide/bitstream/` folder when Vitis prepares the launch. Adjust it to the `.bit` you actually have. |
| Link training fails | Try a different DP cable / monitor, power-cycle the monitor, check the HPD messages on the serial console. |
| Build error with `-lm` search path | Fix `USER_LINK_DIRECTORIES` in `UserConfig.cmake` to your Vitis install path. |
