pkgname=xdg-desktop-portal
pkgver=1.20.3
pkgrel=1
pkgdesc="Desktop integration portals for sandboxed apps"
arch=('x86_64')
url="https://flatpak.github.io/xdg-desktop-portal"
license=('GPL-2.1-or-later')
depends=(
    'fuse'
    'gcc-libs'
    'gdk-pixbuf'
    'glib2'
    'glibc'
    'gstreamer'
    'gst-plugins-base-libs'
    'json-glib'
    'libgudev'
    'libpipewire'
    'pipewire'
    'rtkit'
    'systemd'
    'systemd-libs'
)
makedepends=(
    'bubblewrap'
    'docbook-xsl'
    #'flatpak'
    'geoclue'
    'git'
    'glib2-devel'
    'gst-plugins-good'
    'libportal'
    'meson'
    'python-dbus-python'
    'python-dbusmock'
    'python-docutils'
    'python-pygobject3'
    # 'python-sphinx'
    # 'python-sphinx-copybutton'
    # 'python-sphinxext-opengraph'
    # 'python-sphinx-furo'
    'umockdev'
    'xmlto'
)
source=(git+ssh://git@github.com/flatpak/xdg-desktop-portal#tag=${pkgver})
sha256sums=(f80cf8ff47c09b3ca559095134b505334049adece08cba3be6932d3791e9743c)

prepare() {
    cd ${pkgname}

    # pidfd fixes
    # https://github.com/flatpak/xdg-desktop-portal/issues/1653
    # https://github.com/flatpak/xdg-desktop-portal/pull/1713
    git cherry-pick -n dd08d451e3019f4ec6285ecb14d4c746b6e1d420 \
                       522236e41043a558a825da4cee70ee31ce607147
}

build() {
    cd ${pkgname}

    local meson_args=(
        -D tests=disabled
        -D documentation=disabled
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package() {
    cd ${pkgname}

    ${meson_install} ${pkgdir}
}
