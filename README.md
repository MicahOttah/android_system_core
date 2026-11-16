# android_system_core

Fork of `LineageOS/android_system_core` with the changes of the **LG G Pad
X 8.0 (V521)** port to **LineageOS 15.1** (Android 8.1).

| Branch | What it is |
| --- | --- |
| `lineage-15.1` | the upstream LineageOS 15.1 branch, unchanged |
| `lineage-15.1-v521` | the branch the V521 port builds from |

## What is different on `lineage-15.1-v521`

| Commit | Subject |
| --- | --- |
| `5e3b6fb` | v521: never let the system overwrite the recovery partition |

The recovery partition of this device holds **TWRP**, which was flashed by
hand, not the AOSP recovery that ships with the ROM.  The stock `init.rc`
starts `install-recovery.sh` when `persist.sys.recovery_update` is true,
which would write the ROM's recovery image over the partition and destroy
the TWRP installation.

The trigger is commented out instead of being tied to a property, so that
no build can turn it back on by accident:

```
# update recovery if enabled
#on property:persist.sys.recovery_update=true
#    start flash_recovery
```

## The port

The full description of the port is in the device tree:
<https://github.com/MicahOttah/android_device_lge_v521>
