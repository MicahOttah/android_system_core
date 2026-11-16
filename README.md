# android_system_core

Fork of `LineageOS/android_system_core` with the changes of the **LG G Pad
X 8.0 (V521)** port to **LineageOS 15.1** (Android 8.1).

| Branch | What it is |
| --- | --- |
| `lineage-15.1` | the upstream LineageOS 15.1 branch, unchanged |
| `lineage-15.1-v521` | the branch the V521 port builds from |

## What is different on `lineage-15.1-v521`

Nothing in the code any more; the branch is upstream plus this README.

| Commit | Subject |
| --- | --- |
| `5e3b6fb` | v521: never let the system overwrite the recovery partition |
| (revert) | v521: let the system update the recovery partition again |

`5e3b6fb` commented out the `init.rc` trigger that starts
`install-recovery.sh` when `persist.sys.recovery_update` is true, because the
recovery partition held a hand-flashed TWRP at the time.  The device now runs
the port's own Lineage recovery, which should follow the installed ROM (its
menu prints the ROM version), so the trigger is back as upstream has it:

```
# update recovery if enabled
on property:persist.sys.recovery_update=true
    start flash_recovery
```

The device tree sets `persist.sys.recovery_update=true` by default.

## The port

The full description of the port is in the device tree:
<https://github.com/MicahOttah/android_device_lge_v521>
