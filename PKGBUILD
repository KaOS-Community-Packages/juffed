pkgname=juffed
pkgver=0.10
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
	)
sha512sums=(
	'SKIP'
	'ac9be39d90d5696142b61e00f74577cec23d379be128965642a92cabefd5ed9c511fedeb7cec068f24224d96aa5ace9992920c5a4dd54f90c59a93442f14079a' 
)

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
