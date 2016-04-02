pkgname=gvsig-desktop
pkgver=2.2.0
_pkgrel=2313
pkgrel=1
pkgdesc="A powerful, user-friendly and interoperable GIS."
arch=('x86_64')
url="http://www.gvsig.com/en/products/gvsig-desktop"
license=('GPL')
depends=('java-environment>=6' 'hicolor-icon-theme' 'libidn' 'libldap' 'libjpeg-turbo' 'proj' 'geos' 'openssl')
source=("http://downloads.gvsig.org/download/gvsig-desktop/dists/2.2.0/builds/$_pkgrel/$pkgname-$pkgver-$_pkgrel-final-lin-x86_64.zip"
        "$pkgname.desktop" "gvSIG.config")
sha256sums=('872fee927b1069edcbcfe3fa5f4f6f62afa4b7685bc0e2c8e5836113a4551cab'
            'f3bfca96b53572799aad64092b30ece4cec3b67db0062efada79a48d60d00ea0'
            'd5dd810d2492486af38b2d8079dbd24554b4f7dd6fd43d1af860ae6667239bb2')

package() {
  cd $srcdir
  mkdir -p $pkgdir/opt/$pkgname
  cp -R $srcdir/$pkgname-$pkgver-$_pkgrel-final-lin-x86_64/* $pkgdir/opt/$pkgname


  sed -i  's:"$HOME/$GVSIG_APPLICATION_NAME":$HOME"/.gvsig":' "$pkgdir/opt/$pkgname/gvSIG.sh"

  install -Dm644 "gvSIG.config"  $pkgdir/opt/$pkgname/gvSIG.config

  install -Dm644 "$pkgname.desktop" \
        ${pkgdir}/usr/share/applications/$pkgname.desktop

  install -dm755 ${pkgdir}/usr/bin

  echo "#!/bin/sh" > ${pkgdir}/usr/bin/$pkgname
  echo "/opt/$pkgname/gvSIG.sh" >> ${pkgdir}/usr/bin/$pkgname
  chmod +x ${pkgdir}/usr/bin/$pkgname

  for s in 16 22 48; do
    mkdir -p ${pkgdir}/usr/share/icons/hicolor/${s}x${s}/apps
    cp "${pkgdir}/opt/$pkgname/gvsig-icon${s}x${s}.png" "${pkgdir}/usr/share/icons/hicolor/${s}x${s}/apps/$pkgname.png"
  done

  rm ${pkgdir}/opt/$pkgname/home/gvSIG/plugins/org.gvsig.app.mainplugin/Symbols/Geology/"Neotectonic, Earthquake-Hazard"/Fault-plane*.*
}
