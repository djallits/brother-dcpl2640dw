# Maintainer: Dan Jallits <dan [at] jallits [dot] com>

pkgname=brother-dcpl2640dw
pkgver=4.1.0
pkgrel=1
pkgdesc="CUPS and LPR drivers for the Brother DCP-L2640DW"
arch=("x86_64" "i686")
url="https://support.brother.com/g/b/downloadlist.aspx?c=us&lang=en&prod=dcpl2640dw_us_as&os=127"
license=('GPL-2.0-only' 'custom:Brother EULA')
depends=("cups" "perl")
install="${pkgname}.install"
source=(
    "fix-setupPrintcap.diff"
    "brprintconflsr3_DCPL2640DW"
    "https://download.brother.com/welcome/dlf106025/dcpl2640dwpdrv-${pkgver}-${pkgrel}.i386.rpm"
)
sha256sums=(
    "13ee5b477f1b71e5031e389583852333f69cf218c5bdee0ba30314929117598b"
    "3365c96162ca03866b1a5fc7d8340d9282447d1af4f417adc194898cbbfcff81"
    "0b476e240296deeb0c8135ad0105233f6b93522fa3a4ae85088a175ed3463992"
)

prepare() {
    cd "${srcdir}"
    patch -Np0 < fix-setupPrintcap.diff
}

package() {
    cp -R "${srcdir}/opt" "${pkgdir}/opt"
    local printer_dir="/opt/brother/Printers/DCPL2640DW"

    mv "${pkgdir}/${printer_dir}/lpd/${arch}/"* "${pkgdir}/${printer_dir}/lpd"
    rm -r "${pkgdir}/${printer_dir}/lpd/x86_64"
    rm -r "${pkgdir}/${printer_dir}/lpd/i686"
    ln -s "${printer_dir}/inf/brDCPL2640DWrc" "${pkgdir}/${printer_dir}/lpd/inf/brDCPL2640DWrc"

    install -d "${pkgdir}/usr/lib/cups/filter"
    ln -s "${printer_dir}/cupswrapper/lpdwrapper" "${pkgdir}/usr/lib/cups/filter/brother_lpdwrapper_DCPL2640DW"
    install -d "${pkgdir}/usr/share/cups/model"
    ln -s "${printer_dir}/cupswrapper/brother-DCPL2640DW-cups-en.ppd" "${pkgdir}/usr/share/cups/model"

    install -d "${pkgdir}/usr/bin"
    install -Dm755 "${srcdir}/brprintconflsr3_DCPL2640DW" "${pkgdir}"/usr/bin/
}
