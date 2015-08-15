# Maintainer : speps <speps at aur dot archlinux dot org>
# Contributor: Chris Baker <baker.chris.3@gmail.com>

_name=Editra
pkgname=editra
pkgver=0.7.20
pkgrel=1
pkgdesc="Multi-platform text editor with features that aid in code development"
arch=('any')
url="http://$pkgname.org/"
license=('custom:wxWindows')
depends=('wxpython' 'python2-distribute' 'desktop-file-utils')
install="$pkgname.install"
source=("${url}uploads/src/$_name-$pkgver.tar.gz"
        "$pkgname.desktop")
md5sums=('a52c6b3d703f98e0390aa7b44f991616'
         '6082f8d4bf1650af8ce87c6b3d38053b')
         
build() {
  cd "$srcdir/$_name-$pkgver"
  python2 setup.py build
}

package() {
  cd "$srcdir/$_name-$pkgver"

  python2 setup.py install --root="$pkgdir/"

  # prevent conflicts with wxpython
  mv "$pkgdir/usr/bin/$pkgname" "$pkgdir/usr/bin/$_name"

  # desktop and pixmaps
  install -Dm644 ../${source[1]} "$pkgdir/usr/share/applications/${source[1]}"
  install -Dm644 pixmaps/$pkgname.png "$pkgdir/usr/share/pixmaps/$pkgname.png"

  # license
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"

  # python2 fixes
  sed -i "s|\(^\#\!.*python\).*|\12|" `grep -rl "\#\!.*python" "$pkgdir"`
}
