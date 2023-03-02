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

You can flash them one at a time. Once it's in DFU mode, plug the keyboard half
via USB. It will mount as a flash drive. Copy the corresponding uf2 image, e.g.
sofle_choc_left.uf2 to the left half, and right for the right one. 

After the copy is finished, the drive will automatically unmount. Some desktop
environments will complain about the drive not being safely ejected. That is
not a problem.

[Reference documentation](https://zmk.dev/docs/user-setup)

## Building locally

This is currently for a sofle choc using 
[nice!nano](https://nicekeyboards.com/docs/nice-nano/) and 
[nice!view](https://nicekeyboards.com/docs/nice-view/)

```fish
#!/usr/bin/env fish
cd zmk/app
for side in left right;
    west build -d build/$side -b nice_nano_v2 -- -DSHIELD="sofle_$side nice_view_adapter nice_view" -DZMK_CONFIG=PATH_TO_THIS_REPO/config/; 
end
# You will need to change mount point for each half independently or copy left, 
# then right if you're only flashing one at a time
cp build/left/zephyr/zmk.uf2 NICENANO_MOUNTPOINT
cp build/right/zephyr/zmk.uf2 NICENANO_MOUNTPOINT
```

[Reference documentation](https://zmk.dev/docs/development/setup)
