# Maintainer: Maximilian Luz <luzmaximilian@gmail.com>

pkgname=linux-firmware-ipts-surfacebook2-kbl8
pkgver=20190918T0000
pkgrel=1
pkgdesc="IPTS firmware for the Microsoft Surface Book 2 with 8th gen Kaby-Lake CPU"
arch=('any')
url="https://github.com/ipts-linux-org/ipts-linux-new/wiki"
license=('GPL2' 'custom')
provides=('linux-firmware-ipts')

_tsml_device="MSHW0137"

source=(
    'iaPreciseTouchDescriptor.bin'
    'ipts_fw_config.bin'
    "SurfaceTouchServicingDescriptor${_tsml_device}.bin"
    "SurfaceTouchServicingKernel${_tsml_device}.bin"
    "SurfaceTouchServicingSFTConfig${_tsml_device}.bin"
    "SurfaceTouchServicingTouchBlob${_tsml_device}.bin"
)
sha256sums=('638d44359b1d431c9693034c1f4b104b5378ae3a27fa7a1d81074ac8baba4b16'
            'eed5c04a5f8841d52292fbb321990c79316ce98cd21324c71226cdc95cc20d09'
            '53733fb2156c46508e565489faa9a57f40c2875173ce9aa9cc86bba20fd410d1'
            'dc513b1c65c7ae59575cd1c816e77e96518876d584cbdbae41a044874407e744'
            '11949500a8d706c45e8cb5ed3c090649da02733fcbc635f9f38a66e63cb8ba5c'
            'b57b851d567808906f61a0122273da05c972140f1007355390aaf5dda8a072af')

package() {
    local fwpath="${pkgdir}/usr/lib/firmware/intel/ipts/${_tsml_device}/"

    cd "${srcdir}"
    install -Dm644 "ipts_fw_config.bin" "${fwpath}/ipts_fw_config.bin"
    install -Dm644 "iaPreciseTouchDescriptor.bin" "${fwpath}/intel_desc.bin"
    install -Dm644 "SurfaceTouchServicingKernelMSHW0137.bin" "${fwpath}/vendor_kernel.bin"
    install -Dm644 "SurfaceTouchServicingSFTConfigMSHW0137.bin" "${fwpath}/config.bin"
    install -Dm644 "SurfaceTouchServicingDescriptorMSHW0137.bin" "${fwpath}/vendor_desc.bin"
}
