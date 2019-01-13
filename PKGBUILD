pkgname=brave
pkgver=0.60.11
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (binary release).'
arch=('x86_64')
url='https://brave.com/download'
license=('custom')
depends=('gtk3' 'gconf' 'nss' 'alsa-lib' 'libxss' 'libgnome-keyring' 'ttf-font')
optdepends=('cups: Printer support'
            'pepper-flash: Adobe Flash support')
provides=("${pkgname-bin}" 'brave-browser')
conflicts=("${pkgname-bin}")
source=("$pkgname-$pkgver.zip::https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-v${pkgver}-linux-x64.zip"
	"MPL2::https://raw.githubusercontent.com/brave/brave-browser/master/LICENSE"
        "$pkgname.sh"
        "$pkgname.desktop"
        "logo.png")
options=(!strip)
sha512sums=('fae033454d08b5ac955d4bde303d9c844eb8e3ac21def9133e0e30d1f9c7019e6e08cba9a22fcb12f0b20be0999bc244faccdcb47cb03d6d461f2ecb871d99de'
            'b8823586fead21247c8208bd842fb5cd32d4cb3ca2a02339ce2baf2c9cb938dfcb8eb7b24c95225ae625cd0ee59fbbd8293393f3ed1a4b45d13ba3f9f62a791f'
            'ebe442fc55aa8e32f968c1bf72b154b310b268f69095bb661f8aa1b40c74cc5e4ba5f39425312199e017451f9956d49f40573e5f8b896872f7f722bc6a3d968e'
            'c21aecaafec43bc1ce1ea3439667efb4c7ea5e54bfa87346a9ae9650de1e90c80174b1610a9216f936f693593816c9585c6be1875b3bd318d067079c06251e92'
            'd7bef52e336bd908d24bf3a084a1fc480831d27a3c80af4c31872465b6a0ce39bdf298e620ae9865526c974465807559cc75610b835e60b4358f65a8a8ff159e')
noextract=("$pkgname-$pkgver.zip")

prepare() {
  mkdir -p brave
  cat $pkgname-$pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/$pkgname"

    install -Dm0755 "$pkgname.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "$pkgname.desktop"
    install -Dm0644 "logo.png" "$pkgdir/usr/share/pixmaps/brave.png"
    install -Dm0664 -t "$pkgdir/usr/share/licenses/$pkgname" "MPL2"
    mv "$pkgdir/usr/lib/$pkgname/"{LICENSE,LICENSES.chromium.html} "$pkgdir/usr/share/licenses/$pkgname"

    ln -s /usr/lib/PepperFlash "$pkgdir/usr/lib/pepperflashplugin-nonfree"
}
