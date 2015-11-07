pkgname=juffed
pkgver=0.10.r72.gf638b2c
pkgrel=1
pkgdesc='A lightweight cross-platform text editor. Qt5 UI. Development version.'
arch=('x86_64')
url='http://juffed.com/'
license=('GPL2')
depends=('enca' 'qscintilla-qt5' 'desktop-file-utils')
makedepends=('git' 'cmake' 'qt5-tools')
source=(
	"git+https://github.com/Mezomish/${pkgname}.git"
	"${pkgname}.install"
	"qt5.5.diff"
)
sha512sums=(
	'SKIP'
	'ac9be39d90d5696142b61e00f74577cec23d379be128965642a92cabefd5ed9c511fedeb7cec068f24224d96aa5ace9992920c5a4dd54f90c59a93442f14079a' 'b6f288cf77c382f88322f2e74cf0fbdfc143f495850070939f7bfcb6589d63be393fe2f5050de62298832c89bc82af3e6824029adecacadc9c6bda098bd911f4'
)
/home/chris/builds/juffed/src/juffed/src/3rd_party/qtsingleapplication
pkgver() {
	# Updating package version
	cd ${srcdir}/${pkgname}
	(
		set -o pipefail
		git describe --long --tags 2>/dev/null | sed -r 's/^juffed-//;s/([^-]*-g)/r\1/;s/-/./g' ||
		printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
	)
}

prepare() {
        
	# Make build directory
	mkdir -p ${srcdir}/build
}

build() {
	# Number of jobs
	declare -i njobs=$(nproc)
	
	if [[ ${njobs} -ge 8 ]]; then
		njobs=$(( ${njobs} - 2 ))
	fi
	
	# Building package
	
	cd ${srcdir}/${pkgname}
	patch --binary -p1 -i ../qt5.5.diff
	cd ${srcdir}/build
	cmake ../${pkgname} \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DLIB_INSTALL_DIR=/usr/lib \
		-DUSE_QT5=ON \
		-DUSE_ENCA=ON
	make -j${njobs}
}

package() {
	# Installing package
	cd ${srcdir}/build
	make DESTDIR=${pkgdir} install
}