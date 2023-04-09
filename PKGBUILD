#s This file is part of BlackArch Linux ( https://www.blackarch.org/ ).
# See COPYING for license details.

pkgname=soapysdr
pkgver=0.8.1.r61.g9c4fa32
pkgrel=1
pkgdesc='Vendor and platform neutral SDR support library'
arch=('x86_64' 'aarch64')
groups=('blackarch' 'blackarch-radio')
url='https://github.com/pothosware/SoapySDR'
license=('Boost')
depends=('python')
makedepends=('git' 'cmake' 'swig' 'doxygen' 'graphviz')
optdepends=('soapyairspy: Airspy backend'
            'soapyaudio: Audio devices backend'
            'soapybladerf: BladeRF backend'
            'soapyhackrf: HackRF backend'
            'soapynetsdr: NetSDR backend'
            'soapyosmo: OsmoSDR backend'
            'soapyremote: SoapySDR remote support'
            'soapyrtlsdr: rtl-sdr backend'
            'soapyuhd: UHD backend')
source=("git+https://github.com/pothosware/$pkgname.git")
sha512sums=('SKIP')

pkgver() {
  cd $pkgname

  git describe --long --tags | sed 's/^soapy.sdr-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cmake -B build -S "$pkgname" \
      -DSOAPY_SDR_EXTVER=ARCH \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_BUILD_TYPE=Release

  make -C build
}

check() {
    make -C build test
}

package() {
  make -C build DESTDIR="$pkgdir" install

  install -dm 755 "$pkgdir/usr/share/doc/$pkgname"
  cp -r -a --no-preserve=ownership "build/docs/html" "$pkgdir/usr/share/doc/$pkgname"
}

