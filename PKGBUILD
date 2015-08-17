# Maintainer: Christian Hesse <mail@eworm.de>

pkgname=shrew-vpn-client-unstable
pkgver=2.2.1rc2
pkgrel=1
pkgdesc="A portable VPN client for Linux with Qt GUI - development version"
arch=('i686' 'x86_64')
url="http://www.shrew.net/"
license=('osi')
depends=('qt4' 'openssl')
makedepends=('gcc' 'flex' 'libedit' 'bison' 'cmake')
optdepends=('openldap')
provides=('shrew-vpn-client')
conflicts=('shrew-vpn-client' 'shrew-vpn-client-alpha')
install=shrew-vpn-client.install
backup=('etc/iked.conf')
source=("http://www.shrew.net/download/ike/ike-${pkgver/rc/-rc-}.tbz2"
	'ikea-qt.desktop'
	'iked'
	'iked.service')

build() {
	cd ${srcdir}/ike

	# Build the whole package
	cmake -DCMAKE_INSTALL_PREFIX=/usr -DQTGUI=YES -DETCDIR=/etc -DMANDIR=/usr/share/man -DNATT=YES -DQT_QMAKE_EXECUTABLE=qmake4
	make all
}

package() {
	cd ${srcdir}/ike
	
	make DESTDIR="${pkgdir}/" install
  
	# Install the daemon script und unit file
	install -D -m0755 ${srcdir}/iked ${pkgdir}/etc/rc.d/iked
	install -D -m0644 ${srcdir}/iked.service ${pkgdir}/usr/lib/systemd/system/iked.service

	# The configuration file is already ready for use; just rename it
	mv ${pkgdir}/etc/iked.conf.sample ${pkgdir}/etc/iked.conf

	# Copy our desktop files
	install -D -m0644 ${srcdir}/ike/source/qikea/png/ikea.png ${pkgdir}/usr/share/pixmaps/ikea.png
	install -D -m0644 ${srcdir}/ikea-qt.desktop ${pkgdir}/usr/share/applications/ikea-qt.desktop
}

sha256sums=('c22387eaebdf3f9c93e3a021ab8e8ef83c655929448036f680e2847ffb407a4e'
            '627a3f234f1327cb774146fa4589d170b2a285356d18107bf76059ce0dc4cba2'
            '641909595a5184cee9a11bbc032fc106debb1f95bdbb7c7c4408f9f2a88f7a64'
            '7545cfc878a3375f7ee15b67f4a5c1666d6a96e29f6c71c2dd9778ba7e4f1fe9')
