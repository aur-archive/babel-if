# Maintainer: Brandon Invergo <brandon@invergo.net>
# Contributor: Eric Forgeot < http://ifiction.free.fr >
pkgname=babel-if
pkgver=0.2b
pkgrel=2
epoch=1
pkgdesc="The Treaty of Babel analysis tool for interactive fiction files."
arch=(i686 x86_64)
url="http://babel.ifarchive.org/program.html"
license=('creative-commons-by')
groups=(ifiction)
source=(http://babel.ifarchive.org/downloads/babel.zip http://babel.ifarchive.org/babel_rev7.txt)
md5sums=('a9538dede1c34f544547c44d738c89d2' '86a309d775f822e8c1c8042e0ea1ba16')


build() {
  cd $srcdir/

	sed -i -e "/CC=bcc32/d" makefile
	sed -i -e "/OBJ=.obj/d" makefile
	sed -i -e "/BABEL_LIB=babel.lib/d" makefile
	sed -i -e "/IFICTION_LIB=ifiction.lib/d" makefile
	sed -i -e "/BABEL_FLIB=babel_functions.lib/d" makefile

	sed -i -e "s/#\(CC=gcc -g\)/\1/" makefile
	sed -i -e "s/#\(OBJ=.o\)/\1/" makefile
	sed -i -e "s/#\(BABEL_LIB=babel.a\)/\1/" makefile
	sed -i -e "s/#\(BABEL_FLIB=babel_functions.a\)/\1/" makefile
	sed -i -e "s/#\(IFICTION_LIB=ifiction.a\)/\1/" makefile
	sed -i -e "s/#OUTPUT_BABEL=-o babel/OUTPUT_BABEL=-o babel-if/" makefile

	make || return 1
	cd $srcdir/babel-get
	make || return 1
}

package() {
	mkdir -p $pkgdir/usr/bin
	mkdir -p $pkgdir/usr/share/$pkgname
	mkdir -p $pkgdir/usr/share/doc/$pkgname
	mkdir -p $pkgdir/usr/lib

	cd $srcdir/
	install -D -m755 $srcdir/babel-if $pkgdir/usr/bin/babel-if
	install -D -m755 $srcdir/babel-get/babel-get $pkgdir/usr/bin/babel-get
	install -D -m644 $srcdir/MANIFEST $pkgdir/usr/share/doc/$pkgname/MANIFEST
	install -D -m644 $srcdir/README $pkgdir/usr/share/doc/$pkgname/README
	install -D -m644 $srcdir/babel_rev7.txt $pkgdir/usr/share/doc/$pkgname/babel_rev7.txt
	install -D -m644 $srcdir/babel.a $pkgdir/usr/lib/babel.a
	install -D -m644 $srcdir/babel_functions.a $pkgdir/usr/lib/babel_functions.a
	install -D -m644 $srcdir/ifiction.a $pkgdir/usr/lib/ifiction.a
	cp -fr $srcdir/extras $pkgdir/usr/share/$pkgname
}
