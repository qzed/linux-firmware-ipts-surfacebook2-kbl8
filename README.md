# IPTS Firmware for the Microsoft Surface Book 2 (Kaby Lake, 8th Gen)

Intel Precise Touch & Stylus (IPTS) linux firmware for the Microsoft Surface Book 2 with 8th gen Kaby Lake CPU.

This Package only provides the IPTS firmware.
_Separate GuC firmware for `i915` and a compatible kernel (e.g. [this one][jakeday-linux-surface]) are required for full functionality._
This should usually be provided by your Linux distribution, i.e. for Arch Linux via the `linux-firmware` package (or equivalent).
Specifically, the required files are

- `kbl_dmc_ver1_01.bin`
- `kbl_dmc_ver1_04.bin`
- `kbl_guc_ver9_14.bin`
- `kbl_guc_ver9_39.bin`
- `kbl_huc_ver02_00_1810.bin`

and

- `kbl_dmc_ver1.bin`, which is a symlink to `kbl_dmc_ver1_01.bin` and is apparently required for some kernels.

These files can be found in the [linux firmware repository][firmware-i915-kernel] or via the [official intel page][firmware-i915-intel] and should be placed under `/lib/firmware/i915/`.
_Note: These files are for kaby-lake as indicated by the `kbl` prefix._
_Other processor families require different firmware._

## Instructions

### Arch Linux

Simply use the provided `PKGBUILD`, i.e. clone this repository and then, inside this source directory, run

```shell
makepkg -si
```

If not present, install `linux-firmware` or an equivalent package as mentioned above.

### Manual Installation

Copy the `*.bin` files to `/lib/firmware/intel/ipts/` and create the following symlinks

```shell
cd /lib/firmware/intel/ipts
ln -s SurfaceTouchServicingDescriptorMSHW0137.bin vendor_desc.bin
ln -s SurfaceTouchServicingKernelMSHW0137.bin vendor_kernel.bin
ln -s SurfaceTouchServicingSFTConfigMSHW0137.bin config.bin
ln -s iaPreciseTouchDescriptor.bin intel_desc.bin
```

## Sources

This package is based on the following documentation, credits apply:

- [Intel's IPTS for Linux wiki][ipts-linux-wiki]
- [Jake Day's Linux kernel for Surface devices][jakeday-linux-surface]

### Obtaining the Firmware Files

As described [here][ipts-linux-wiki], the firmware files can be obtained from a Windows installation.
They are placed in `%WINDIR%\INF\PreciseTouch\Intel\`.
For some versions, the `iaPreciseTouchDescriptor.bin` does not seem to be present.
If this is the case, it can be obtained from [here][jakeday-linux-surface-firmware] or [here][axelrtgs-linux-firmware]:

### Different Surface Book Versions

See the [Intel IPTS for Linux wiki][ipts-linux-wiki].
Basically, obtain the respective firmware files from a Windows installation as described above.
The only difference should be the names of the files, they can be installed equivalently.
You can alternatively consult Jake Day's [linux-surface repo][jakeday-linux-surface], specifically the `setup.sh` script and `firmware` directory.

## License

This package is provided under the GPLv2 license, except for the actual firmware files (`*.bin`) bundeled with it.
All rights to these files lay with Microsoft and/or their respecitve vendors.
They are only bundeled for convenience.
Anyone who can make use of these files needs specific hardware, which inherently provides access to these files through the included windows installation (see above).

[firmware-i915-kernel]: https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/i915
[firmware-i915-intel]: https://01.org/linuxgraphics/downloads/firmware
[ipts-linux-wiki]: https://github.com/ipts-linux-org/ipts-linux-new/wiki
[jakeday-linux-surface]: https://github.com/jakeday/linux-surface
[jakeday-linux-surface-firmware]: https://github.com/jakeday/linux-surface/tree/master/firmware
[axelrtgs-linux-firmware]: https://github.com/axelrtgs/linux-firmware-ipts/tree/master/intel/ipts
