# zmk-config
Personal keymaps to use as zmk-config

## Github actions

Github will build this repository automatically when code is pushed. The
result will be in a firmware.zip that will contain uf2 files for both halves.
Resetting the nice!nano controller while still in reset will put it in "DFU"
mode. This can be achieved by "double clicking" the reset button on the sofle
choc. The blue LED should remain blinking when in DFU mode. If it only blinks a
couple times, it means that it only reset and you can try double clicking
again.

## Building locally

This is currently for a sofle choc using 
[nice!nano](https://nicekeyboards.com/docs/nice-nano/) and 
[nice!view](https://nicekeyboards.com/docs/nice-view/)

```fish
cd zmk/app
for side in left right; west build -d build/$side -b nice_nano_v2 -- -DSHIELD="sofle_$side nice_view_adapter nice_view" -DZMK_CONFIG=PATH_TO_THIS_REPO/config/; end
cp build/left/zephyr/zmk.uf2 NICENANO_MOUNTPOINT
cp build/right/zephyr/zmk.uf2 NICENANO_MOUNTPOINT
```
