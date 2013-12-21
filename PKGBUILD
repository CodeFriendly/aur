# Maintainer: Robert Holak <rholak@gmail.com>
pkgname=greyhole
pkgver=0.9.35
pkgrel=1
pkgdesc="Greyhole is an application that uses Samba to create a storage pool of all your available hard drives and allows you to create redundant copies of the files you store, in order to prevent data loss when part of your hardware fails."
url="http://greyhole.net"
arch=('x86_64' 'i686')
license=('GPLv3')
depends=('php' 'php-intl' 'samba' 'mysql' 'rsync' )
backup=("etc/greyhole.conf")
install='greyhole.install'
source=("http://www.greyhole.net/releases/${pkgname}-${pkgver}.tar.gz"
"greyhole.service")

md5sums=('987c5a7842a19561d045da28053cf97c'
         '2fed371aa5cb4d71bc34390d0d5688da')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  mkdir -p $pkgdir/var/spool/greyhole
  chmod 777 $pkgdir/var/spool/greyhole

  install -m 0755 -D -p greyhole $pkgdir/usr/bin/greyhole
  install -m 0755 -D -p greyhole-dfree $pkgdir/usr/bin/greyhole-dfree
  #install -m 0750 -D -p greyhole-config-update $pkgdir/usr/bin/greyhole-config-update
  install -m 0644 -D -p logrotate.greyhole $pkgdir/etc/logrotate.d/greyhole
  install -m 0644 -D -p greyhole.cron.d $pkgdir/etc/cron.d/greyhole
  install -m 0644 -D -p greyhole.example.conf $pkgdir/etc/greyhole.conf
  install -m 0755 -D -p greyhole.cron.weekly $pkgdir/etc/cron.weekly/greyhole
  install -m 0755 -D -p greyhole.cron.daily $pkgdir/etc/cron.daily/greyhole
  install -m 0644 -D -p docs/greyhole.1.gz $pkgdir/usr/share/man/man1/greyhole.1.gz
  install -m 0644 -D -p docs/greyhole-dfree.1.gz $pkgdir/usr/share/man/man1/greyhole-dfree.1.gz
  install -m 0644 -D -p docs/greyhole.conf.5.gz $pkgdir/usr/share/man/man5/greyhole.conf.5.gz
  install -m 0755 -D -p $startdir/greyhole.service $pkgdir/usr/lib/systemd/system/greyhole.service
  install -m 0644 -D -p schema-mysql.sql $pkgdir/usr/share/greyhole/schema-mysql.sql
  install -m 0644 -D -p USAGE $pkgdir/usr/share/greyhole/USAGE

  #Choose correct samba module
  if [ "$CARCH" = "i686" ] ; then
    vfs_file=greyhole-i386.so
  else
    vfs_file=greyhole-x86_64.so
  fi

  install -m 0644 -D -p samba-module/bin/4.0/$vfs_file $pkgdir/usr/lib/samba/vfs/greyhole.so

}

# vim:set ts=2 sw=2 et:
