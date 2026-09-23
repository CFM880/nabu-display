# nabu-display

**English** | 中文

SM8150 display support for the Xiaomi Pad 5 (`nabu`): the DPU/DSI changes, the
Novatek NT36523 panel driver and the DRM notifier that lets the panel notify the
touchscreen when it is turned on.

This is a direct source overlay, like the other `nabu-*` repositories: kernel
files keep their original relative paths and are copied over a chosen kernel
baseline by `nabu-main`. It contains no kernel tree, UKI or module tree.

## Contents

```text
kernel-overlay/
├── Documentation/devicetree/bindings/display/panel/novatek,nt36523.yaml
├── drivers/gpu/drm/Makefile
├── drivers/gpu/drm/drm_notifier.c
├── drivers/gpu/drm/msm/disp/dpu1/...            # active-CTL and SSPP changes
├── drivers/gpu/drm/msm/dsi/dsi_manager.c
├── drivers/gpu/drm/panel/panel-novatek-nt36523.c
└── include/drm/drm_notifier.h
config/nabu-display.config
```

## Notes

- The DPU/DSI stack and the panel are built in (`CONFIG_DRM_MSM=y`,
  `CONFIG_DRM_PANEL_NOVATEK_NT36523=y`), so this module produces no `.ko`; it is
  an overlay plus a config fragment.
- The active-CTL changes touch several DPU catalogs (`dpu_5_0_sm8150.h` through
  `dpu_9_0_sm8550.h`), so keeping them here also affects other SoCs' catalogs.
- The panel driver comes from the SM8150 port range; the device tree node lives
  in `nabu-platform` (`sm8150-xiaomi-nabu.dts`).
