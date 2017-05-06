pkgname=insync
pkgver=1.3.16
_pkgver=36155
pkgrel=1
pkgdesc="An unofficial Google Drive client that runs on Linux, with support for various desktops"
url="https://www.insynchq.com/downloads"
license=('custom:insync')
depends=('xdg-utils' 'glibc' 'python2')
arch=('x86_64')
source=('insync@.service' 'insync.service')
source=("http://s.insynchq.com/builds/${pkgname}_${pkgver}.${_pkgver}-trusty_amd64.deb")
sha256sums=('0d8579421818f5583505fba183f7ffd73066ae53a6e831a0b5b34ef6100eeb7e'
            'cf276c1dbf1592ea63a21c2d61c75f7ad6ec3b13e87b3aaa331e9c14799f4598'
            '1432141539a6b3c5333631a2ee6696fab9bd2fe8770643bc670d95e4e96203e0')

package() {
   tar xvf data.tar.gz
   cp -rp usr $pkgdir

   # Patch files for Arch
   cd $pkgdir
   echo "==> Patching files..."
   for file in $(grep -R "/usr/bin/python" . | cut -f1 -d :)
   do
      grepPrefix=$(echo $file | cut -f1 -d" ")
      [ -z $grepPrefix ] && sed -i "s|usr/bin/python$|usr/bin/python2|g" $file
   done
   # End of patching

   mkdir -p ${pkgdir}/usr/lib/systemd/system
   mkdir -p ${pkgdir}/usr/lib/systemd/user
   cp ${srcdir}/insync@.service ${pkgdir}/usr/lib/systemd/system/insync@.service
   cp ${srcdir}/insync.service ${pkgdir}/usr/lib/systemd/user/insync.service
   ln -sf "/usr/lib/libfontconfig.so.1" "${pkgdir}/usr/lib/insync/libfontconfig.so.1"
}
