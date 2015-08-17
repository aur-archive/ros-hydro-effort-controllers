
pkgdesc="ROS - effort_controllers."
url='http://www.ros.org/'

pkgname='ros-hydro-effort-controllers'
pkgver='0.6.0'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-control-toolbox
  ros-hydro-forward-command-controller
  ros-hydro-realtime-tools
  ros-hydro-catkin
  ros-hydro-controller-interface
  ros-hydro-dynamic-reconfigure
  ros-hydro-urdf
  ros-hydro-control-msgs)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-hydro-control-toolbox
  ros-hydro-forward-command-controller
  ros-hydro-realtime-tools
  ros-hydro-controller-interface
  ros-hydro-dynamic-reconfigure
  ros-hydro-urdf
  ros-hydro-control-msgs)
depends=(${ros_depends[@]})

_tag=release/hydro/effort_controllers/${pkgver}-${_pkgver_patch}
_dir=effort_controllers
source=("${_dir}"::"git+https://github.com/ros-gbp/ros_controllers-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
