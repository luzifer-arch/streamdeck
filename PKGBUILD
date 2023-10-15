# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=streamdeck
pkgver=1.7.1
pkgrel=1
pkgdesc="Utility to control Elgato StreamDeck on Linux"
arch=('i686' 'x86_64')
conflicts=('streamdeck-ui')
url="https://github.com/Luzifer/$pkgname"
license=('Apache')
depends=(hidapi)
makedepends=('go')
source=(
  "${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
  "50-streamdeck.rules"
)
sha512sums=('52380fbb3f1119b0fa16ee4bf8b1812a4415da50c30e6d15a6e6e8607d06dfd871eb8847f2f3bd1ff5fd86da7bc455cf0933bde31bf8640d23515468393676be'
            'e3328d8b770a1393a71a95e7be86f88feb3014fda82dc7a4b4c0721b3a8baf84890af3bd639d3e096c31e5c23ff1f345c8cc9216114039cca32f03a360046ddc')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}/cmd/streamdeck"
  go build \
    -buildmode=pie \
    -ldflags="-X main.version=${pkgver}" \
    -mod=readonly \
    -trimpath
}

package() {
  install -Dm755 -t "${pkgdir}/usr/bin" "${srcdir}/${pkgname}-${pkgver}/cmd/streamdeck/streamdeck"
  install -Dm644 -t "${pkgdir}/usr/share/licenses/${pkgname}" "${srcdir}/${pkgname}-${pkgver}/LICENSE"
  install -Dm644 -t "${pkgdir}/etc/udev/rules.d" "${srcdir}/50-streamdeck.rules"
}
