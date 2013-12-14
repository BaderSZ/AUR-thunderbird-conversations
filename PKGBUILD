# Maintainer: Daniel Landau <daniel.landau@iki.fi>

pkgname=thunderbird-conversations-git
pkgver=r1302.d41cbd2
pkgrel=1
pkgdesc="GMail-like conversation view for Thunderbird"
arch=('any')
url="https://github.com/protz/GMail-Conversation-View"
license=('MPL' 'GPL2' 'LGPL2.1')
depends=('thunderbird')
makedepends=('git' 'nodejs')
source=("$pkgname"::'git://github.com/protz/GMail-Conversation-View.git')
md5sums=('SKIP')
pkgver() {
        cd "$srcdir/$pkgname"
        printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}
prepare() {
        cd "$srcdir/$pkgname"
        git submodule init
        git submodule update
}

build() {
        cd "$srcdir/$pkgname"
        pushd content/pdfjs
        node make generic
        popd
        ./build.sh
}

package() {
        cd "$srcdir/$pkgname"
        emid="$(sed -n '/.*<em:id>\(.*\)<\/em:id>.*/{s//\1/p;q}' install.rdf)"

        install -d -m755 "$pkgdir"/usr/lib/thunderbird/extensions/"$emid"
        cd "$pkgdir"/usr/lib/thunderbird/extensions/"$emid"

        unzip "$srcdir/$pkgname/conversations.xpi"
}
