# Maintainer: hyknn <hyknn@protonmail.com>
pkgname=obs-plugin-vertical-canvas-git
_pkgname=obs-vertical-canvas
pkgver=1.5.2.r0.gcdb7b4f
pkgrel=1
pkgdesc='Plugin for OBS Studio to add vertical canvas by Aitum'
arch=('x86_64')
url='https://github.com/Aitum/obs-vertical-canvas'
license=('GPL2')
groups=('obs-plugins')
depends=(
	'obs-studio>=30.0.0'
    'qt6-base'
    'curl'
)
makedepends=(
	'cmake'
	'make'
	'gcc'
	'git'
)
provides=('obs-plugin-vertical-canvas')
conflicts=()
options=()
source=('git+https://github.com/Aitum/obs-vertical-canvas.git#branch=main')
sha256sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_pkgname}"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "${srcdir}/${_pkgname}"
    sed -i '/find_qt(COMPONENTS Widgets Core)/,/else()/d' CMakeLists.txt
}

build() {
	cd "${srcdir}/${_pkgname}"
	cmake -S . -B build -DBUILD_OUT_OF_TREE=On
	cmake --build build
}

package() {
    _prjdir="${srcdir}/${_pkgname}"
    install -D -m755 "${_prjdir}/build/vertical-canvas.so" "${pkgdir}/usr/lib/obs-plugins/aitum-vertical-canvas.so"
    install -D -m644 "${_prjdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    mkdir -p "${pkgdir}/usr/share/obs/obs-plugins/aitum-vertical-canvas"
    cp -r "${_prjdir}/data/locale" "${pkgdir}/usr/share/obs/obs-plugins/aitum-vertical-canvas/locale"
}
