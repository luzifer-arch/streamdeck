# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=streamdeck
pkgver=1.7.2
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
sha512sums=('fe22fe9d272369074955c4439b801ea78614e758e5c6ec984a083e88b10d1f2b6ed9705bcce84c2f9f94d605ca26d2ef2e6eb676a9f47b1edebaa80d22d8150f'
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
