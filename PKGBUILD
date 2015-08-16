# Maintainer : Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=konversation-frameworks-git
pkgver=r8003.4b1b3c3
pkgrel=1
pkgdesc="A user friendly IRC client for KF5 Frameworks. (GIT Version)"
arch=('x86_64' 'i686')
url="http://konversation.kde.org"
makedepends=('git' 'extra-cmake-modules' 'kdoctools' 'python')
depends=('knotifyconfig' 'kemoticons' 'kparts' 'kidletime' 'qca-qt5')
optdepends=('python: python scripting support')
conflicts=('konversation')
provides=('konversation')
license=('GPL2' 'FDL')
install=konversation-git.install
source=('git://anongit.kde.org/konversation')
sha1sums=('SKIP')
_gitname=konversation

pkgver() {
  cd "${_gitname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  rm -fr build
  mkdir -p build
  sed 's|find_package(Qca 2.1.0)|find_package(Qca-qt5 2.1.0)|g' -i "${_gitname}/CMakeLists.txt"
}

build() {
  cd build

  cmake "../${_gitname}" \
      -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DLIB_INSTALL_DIR=lib \
      -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
      -DQca-qt5_DIR=/usr/lib/cmake/Qca
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
