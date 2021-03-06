pkgdesc="ROS - Generalized client side source for rosserial."
url='https://wiki.ros.org/rosserial_client'

pkgname='ros-noetic-rosserial-client'
pkgver='0.9.1'
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
    ros-noetic-rosbash
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-rosserial-msgs
    ros-noetic-std-msgs
    ros-noetic-rospy
    ros-noetic-tf
    ros-noetic-rosunit
)

depends=(
	${ros_depends[@]}
)

_dir="rosserial-${pkgver}/rosserial_client"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-drivers/rosserial/archive/${pkgver}.tar.gz")
sha256sums=('0e4dbb4d6e456c354ee04f552cc36b43d053dc3f5a8bbfccff7f8adf3ae48534')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
