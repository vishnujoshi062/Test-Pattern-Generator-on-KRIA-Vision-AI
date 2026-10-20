# Vitis part (steps 3-8)

Expected workspace layout (names matter, because `launch.json` refers to them):

```
<workspace>/
├── platform_ps/               <- platform component built from ../vivado/design_1_wrapper.xsa
└── xdpdma_video_example/      <- application component (DPDMA example from the BSP)
```

Files in this repo that you copy into the application component:

| Repo file | Destination in the Vitis app component |
|-----------|----------------------------------------|
| `xdpdma_video_example/src/xdpdma_video_example.c` | `src/` |
| `xdpdma_video_example/src/xdpdma_video_example.h` | `src/` |
| `xdpdma_video_example/src/xdppsu_interrupt.c`     | `src/` |
| `xdpdma_video_example/src/UserConfig.cmake`       | `src/` (shown as *Settings > UserConfig.cmake*) |
| `xdpdma_video_example/_ide/launch.json`           | `_ide/` (shown as *Settings > launch.json*) |

`launch.json` uses `${workspaceFolder}` so it works with any workspace location, as long as the
platform is called `platform_ps` and the app `xdpdma_video_example`.
**Edit `UserConfig.cmake`**: `USER_LINK_DIRECTORIES` points to the original author's Vitis install
(`E:/Vitis/2024/gnu/aarch64/nt/aarch64-none/aarch64-xilinx-elf/usr/include`); change it to your own install.

## Code change
Only one call changed compared to the stock example (see `../patches/tpg_input_select.patch`):

```c
// stock
XAVBuf_InputVideoSelect(AVBufPtr, XAVBUF_VIDSTREAM1_NONE, XAVBUF_VIDSTREAM2_NONLIVE_GFX);
// this repo: show the Test Pattern Generator (TPG) on video stream 1
XAVBuf_InputVideoSelect(AVBufPtr, XAVBUF_VIDSTREAM1_TPG, XAVBUF_VIDSTREAM2_NONE);
```
