# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=streamdeck
pkgver=1.7.0
pkgrel=3
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
sha512sums=('46d5c68212231ef10f00eea034353c3e42e211ac63c8461d3654c6f46e47f626f69e9564ba91165c8ef47ef0c53c3fbfbb7c9d8ca7c9550e830210e74075a5e5'
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
