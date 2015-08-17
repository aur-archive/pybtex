# Maintainer: Fabio Zanini <fabio.zanini@fastmail.fm>
pkgname=pybtex
pkgver=0.15
pkgrel=1
pkgdesc="Pybtex reads citation information from a file and produces a formatted bibliography."
arch=('i686' 'x86_64')
url="https://code.launchpad.net/pybtex"
license=('GPL')
depends=('python2' 'bzr')
source=() # Bazaar is used to get this dynamically
md5sums=() # Bazaar is used to check this dynamically

_bzrbranch=lp:pybtex
_bzrname=pybtex

build() {
  msg "Connecting to the server...."

  if [ -d ${srcdir}/${_bzrname} ] ; then
    cd ${_bzrname} && bzr pull ${_bzrbranch}
    msg "Local repository updated."
  else
    bzr co ${_bzrbranch}
  fi

  msg "BZR checkout done or server timeout"

  msg "Starting make..."
  cd "${srcdir}/${_bzrname}"

  # Replace python with python2
  for file in $(find $srcdir/$_bzrname -name '*.py' -print); do
      sed -i 's_^#!.*/usr/bin/python_#!/usr/bin/python2_' $file
      sed -i 's_^#!.*/usr/bin/env.*python_#!/usr/bin/env python2_' $file
  done
}

package() {
  cd "${srcdir}/${_bzrname}"
  python2 setup.py install --prefix'=/usr' --root="${startdir}/pkg" || return 1
}
