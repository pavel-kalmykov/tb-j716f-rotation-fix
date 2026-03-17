# TB-J716F Rotation Fix

Magisk module for the Lenovo Xiaoxin Pad Pro 2021 (TB-J716F). Fixes the broken screen orientation that shows up when you run a TrebleDroid GSI on this tablet.

## What's the problem?

The TB-J716F has a landscape panel (2560x1600) physically mounted at 270 degrees. Stock ZUI knows about this quirk, but AOSP and GSI ROMs don't. The result:

- The boot animation plays sideways
- The lock screen is stuck in portrait and won't rotate
- System UI and Settings default to the wrong orientation

## What does this module fix?

Three things:

1. **Boot animation orientation.** Sets `ro.bootanim.set_orientation` for both the logical display ID (Android 14 QPR2+) and the physical display ID (Android 13/14 QPR1), so the animation renders correctly across versions.

2. **Lock screen rotation.** Enables `lockscreen.rot_override=true`, which tells AOSP's KeyguardStateController to actually respect the accelerometer on the lock screen.

3. **Rotation mapping and defaults.** Installs two RRO overlays from TrebleDroid that correct the rotation direction and set sane default orientation values.

## Compatibility

| | |
|---|---|
| **Device** | Lenovo Xiaoxin Pad Pro 2021 / Lenovo Tab P11 Pro (TB-J716F, SM8250) |
| **ROMs** | TrebleDroid GSIs: DerpFest, CrDroid, LineageOS GSI, etc. |
| **Android** | 13, 14, 15, 16 |
| **Root** | Magisk 20.4+ |

Other landscape tablets with `installOrientation` might benefit too, but the display ID property in `system.prop` is specific to this device.

## Installation

1. Grab the zip from [Releases](https://github.com/pavel-kalmykov/tb-j716f-rotation-fix/releases)
2. In Magisk: Modules > Install from storage > pick the zip
3. Reboot

The module also supports Magisk's OTA update checker, so you'll get notified when a new version is out.

## What's inside

```
module.prop          Module metadata + OTA update URL
system.prop          Boot animation and lock screen properties
system/product/overlay/
  treble-overlay-tablet-reverse-rotation.apk    Rotation mapping (from TrebleDroid)
  treble-overlay-tablet-settings-defaults.apk   Default orientation (from TrebleDroid)
```

No scripts, no SELinux patches, no background services. Just properties and overlays.

## Credits

- [phhusson / TrebleDroid](https://github.com/phhusson/treble_experimentations) for the RRO overlay APKs
- [topjohnwu](https://github.com/topjohnwu/Magisk) for Magisk

## License

Apache 2.0. See [LICENSE](LICENSE).
