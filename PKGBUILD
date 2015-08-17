# Maintainer: TZ86
# Contributor: ruario
pkgname=opera-dev # Set to "opera" or "opera-next" if you want to replace either of these
_bigrelease=12.15
_buildver=1745
_randomizer=noserch
pkgver=${_bigrelease}_${_buildver}
pkgrel=1
pkgdesc="A fast and secure web browser and Internet suite. Development snapshot of stable branch."
url="http://www.opera.com/browser/"
depends=('gcc-libs' 'libxt' 'freetype2' 'libxext')
provides=('opera')
optdepends=('gstreamer0.10-base-plugins: HTML5 Video support' 'gstreamer0.10-good: HTML5 Video support')
install=opera-dev.install
options=(!strip !zipman)
license=('custom:opera')
arch=('i686' 'x86_64')
_arch=i386
[ "$CARCH" = "x86_64" ] && _arch=x86_64
source=(http://snapshot.opera.com/unix/${_randomizer}_${_bigrelease}-${_buildver}/opera-${_bigrelease}-${_buildver}.${_arch}.linux.tar.xz http://people.opera.com/ruario/opera-next-icons_20111107.tar.xz)
sha256sums=('e2bc5d10b462da9987a137cc0229d2dda2dcf33eca67dad9f4ee8b79f7358581' '4040aad19e11c6e32d3603467858bf58dd389b24a4314e7cbb8b86c9c7b689fd')
[ "$CARCH" = "x86_64" ] && sha256sums=('56deed8b324cb0d909988abe7e3e5a6cc9d753b6e34422266ddedd8a7b898216' '4040aad19e11c6e32d3603467858bf58dd389b24a4314e7cbb8b86c9c7b689fd')
 
# Uncomment the following line, if you want your User Agent to include Arch Linux.
#_opdistro="Arch Linux"
 
package() {
        opera-${_bigrelease}-${_buildver}.${_arch}.linux/install --prefix /usr --name ${pkgname} --repackage "${pkgdir}/usr"
        install -D -m 644 "${pkgdir}/usr/share/${pkgname}/defaults/license.txt" "${pkgdir}/usr/share/licenses/${pkgname}/license.txt"
        
        # User Opera Next icon set if package name is set to Opera Next
        if [ "${pkgname}" = "opera-next" ]; then
                tar -xf opera-next-icons_20111107.tar.xz -C "${pkgdir}"
                sed -i "s/^\(Product=\)opera$/\1opera-next/" "${pkgdir}/usr/share/opera-next/package-id.ini"
        fi
        
        # Insert an Arch User Agent string if set
        if [ -n "${_opdistro}" ]
        then
                mkdir -p "${pkgdir}/usr/share/${pkgname}/custom/defaults"
                echo "[ISP]" > "${pkgdir}/usr/share/${pkgname}/custom/defaults/operaprefs.ini"
                echo "Id=${_opdistro}" >> "${pkgdir}/usr/share/${pkgname}/custom/defaults/operaprefs.ini"
                chmod 644 "${pkgdir}/usr/share/${pkgname}/custom/defaults/operaprefs.ini"
        fi
}
