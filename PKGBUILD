# Maintainer: Anastasios Vacharakis <archlinux@vacharakis.de>

pkgname=steamdeck-gyrodsu
pkgver=2.1.1
pkgrel=1
pkgdesc="A tool for enabling gyroscopic controls on Steam Deck."
arch=('x86_64')
url="https://github.com/kmicki/SteamDeckGyroDSU"
license=('MIT')
makedepends=('git' 'make' 'gcc' 'glibc' 'linux-api-headers' 'ncurses' 'systemd-libs' 'hidapi')
source=("$pkgname::git+${url}")
sha256sums=('SKIP')

prepare() {
    git -C "${pkgname}" switch --detach "v${pkgver}"
}

build() {
    make -C "${pkgname}" release
    sed -i 's|ExecStart=%h/sdgyrodsu/sdgyrodsu|ExecStart=/usr/bin/sdgyrodsu|' "${pkgname}/pkg/sdgyrodsu.service"
}

package() {
    install -Dm755 "${pkgname}/bin/release/sdgyrodsu" "${pkgdir}/usr/bin/sdgyrodsu"
    install -Dm644 "${pkgname}/pkg/sdgyrodsu.service" "${pkgdir}/usr/lib/systemd/user/sdgyrodsu.service"
}

post_install() {
    echo "To enable and start SteamDeckGyroDSU, run:"
    echo "systemctl --user enable sdgyrodsu.service"
    echo "systemctl --user start sdgyrodsu.service"
}
