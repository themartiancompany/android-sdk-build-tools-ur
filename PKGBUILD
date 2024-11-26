# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Amin Vakil <info AT aminvakil DOT com>
# Contributor: xgdgsc <xgdgsc @t gmail dot com>
# Contributor: mynacol <dc07d át mynacol dót xyz>

pkgname=android-sdk-build-tools
# _ver="$( \
#   cat \
#     "${srcdir}/$_android/source.properties" | \
#     grep \
#       ^Pkg.Revision= | \
#       sed \
#         's/Pkg.Revision=\([0-9.]*\).*/\1/')"
_major=34
_minor=0
_micro=0
_ver=34.0.0
_displayversion=34
pkgver=r34.0.0
pkgrel=2
_sdk=android-sdk
_android=android-14
_pkgdesc=(
  'Build-Tools for Google Android SDK'
  '(aapt, aidl, dexdump, dx, llvm-rs-cc)'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'i686'
  'aarch64'
  'arm'
  'armv7l'
)
url="https://developer.android.com/studio/releases/build-tools"
license=(
  'custom'
)
depends=(
  'gcc-libs'
  'zlib'
  'bash'
)
optdepends=(
  'lib32-gcc-libs'
  'lib32-zlib'
  'java-runtime'
)
_android_repo="https://dl.google.com/android/repository"
source=(
  "${_android_repo}/build-tools_r${_displayversion}-linux.zip"
   "package.xml"
)
sha512sums=(
  'c28dd52f8eca82996726905617f3cb4b0f0aee1334417b450d296991d7112cab1288f5fd42c48a079ba6788218079f81caa3e3e9108e4a6f27163a1eb7f32bd7'
  '501211771b02940010420a4003b8396d3d6599fb339c2f64959335ab1c3cf615811cc62acaa093c9f4e14bbc019a9e493835573a5136383617d8b5184509d3f8'
)
options=(
  '!strip'
)

package() {
  local \
    _binaries=() \
    _f \
    _target
  cd \
    "$pkgdir"
  install \
    -d \
    "usr/share/licenses/${pkgname}/"
  ln \
    -s \
    "/opt/${_sdk}/build-tools/${_ver}/NOTICE.txt" \
    "usr/share/licenses/${pkgname}/NOTICE.txt"
  sed \
    -i \
    "s/@major@/${_major}/g;
     s/@minor@/${_minor}/g;
     s/@micro@/${_micro}/g;
     s/@displayv@/${_displayversion}/g;
     s/@pathv@/${_ver}/g" \
     "${srcdir}/package.xml"
  install \
    -Dm644 \
    "${srcdir}/package.xml" \
    "opt/${_sdk}/build-tools/${_ver}/package.xml"
  ln \
    -s \
    "/opt/${_sdk}/build-tools/${_ver}/package.xml" \
    "usr/share/licenses/${pkgname}/package.xml"
  _target="opt/${_sdk}/build-tools/${_ver}"
  mkdir \
    -p \
    "${_target}"
  cp \
    -r \
    "${srcdir}/${_android}/"* \
    "${_target}"
  chmod \
    +Xr \
    -R \
    "${_target}"
  # Add symlinks to binaries to usr/bin/
  mkdir \
    -p \
    "usr/bin/"
  # lld is also provided by
  # extra/lld, not creating symlink
  _binaries=( $( \
    find \
      "${_target}" \
      -maxdepth \
        1 \
      -type \
        "f" \
      -executable \
      -not \
      -iname \
        "lld" \
      -printf \
        "%f\n")
  )
  for _f in ${_binaries[@]}; do
    ln \
      -s \
      "/${_target}/${_f}" \
      "usr/bin/${_f}"
  done
}

