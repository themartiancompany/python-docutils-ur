#g SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Felix Yan
#     <felixonmars@archlinux.org>
#   Daniel M. Capella
#     <polyzen@archlinux.org>
# Contributors:
#   Sébastien Luttringer
#   Ionut Biru
#     <ibiru@archlinux.org>
#   Sergej Pupykin
#     <pupykin.s+arch@gmail.com>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="gitlab"
fi
if [[ ! -v "_git_http" ]]; then
  if [[ "${_git_service}" == "gitlab" ]]; then
    _git_http="gitlab.com"
  elif [[ "${_git_service}" == "github" ]]; then
    _git_http="github.com"
  elif [[ "${_git_service}" == "svn" ]]; then
    # Repo
    _git_http="repo.or.cz"
  fi
fi
if [[ ! -v "_source" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _source="gitlab"
  elif [[ "${_git}" == "false" ]]; then
    _source="sourceforge"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_source}" == "sourceforge" ]]; then
      _archive_format="tar.gz"
    else
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _archive_format="tar.gz"
      fi
    fi
  fi
fi
_py="python"
_pyver="$(
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$((
  ${_pyminver} + 1))"
_pkg=docutils
_proj=hip
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
_commit="ab29cf78ae24a9970d9884de40926dceb855bd32"
pkgver=0.21.2
pkgrel=28
epoch=1
_pkgdesc=(
  'Set of tools for processing plaintext'
  "docs into formats such as HTML, XML, or LaTeX"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
if [[ ! -v "_ns" ]]; then
  _ns=""
  if [[ "${_git_service}" == "gitlab" || \
        "${_git_service}" == "github" ]]; then
    _ns="themartiancompany"
  fi
fi
url="http://${_pkg}.sourceforge.net"
_url="https://${_git_http}/${_ns}/${_pkg}"
if [[ "${_git_service}" == "gitlab" || \
      "${_git_service}" == "github" ]]; then
  url="${_url}"
fi
license=(
  'custom'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pillow"
)
_myst_parser_optdepends=(
  "${_py}-myst-parser:"
    "to parse input in 'Markdown' (CommonMark) format."
)
_pillow_optdepends=(
  "${_py}-pillow:"
    "for some image manipulation operations."
)
_pygments_optdepends=(
  "${_py}-pygments:"
    "for syntax highlighting of code directives and roles."
)
optdepends=(
  "${_myst_parser_optdepends[*]}"
  "${_pillow_optdepends[*]}"
  "${_pygments_optdepends[*]}"
)
_sf="https://downloads.sourceforge.net"
source=(
  "${_sf}/${_pkg}/${_pkg}-$pkgver.tar.gz"
)
source=()
sha256sums=()
_url="${url}"
if [[ "${_git}" == "true" ]]; then
  _tag="${_commit}"
  _tag_name="commit"
elif [[ "${_git}" == "false" ]]; then
  _tag="${pkgver}"
  _tag_name="pkgver"
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_release_sum="3a6b18732edf182daa3cd12775bbb338cf5691468f91eeeb109deff6ebfa986f"
_release_sig_sum="68cb775a1caf5b122f92a93b7d9287ea903abfbe1ad13f54fb7e1d79736c437b"
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum='SKIP'
_github_sig_sum="SKIP"
_release_b2_sum='727c2f97fc5835a0ffa62e38ea85af366cd89ad1eaec0b8af8b1f3b12e6cddfddb65161ba34f9109952d37ba2cf8985f3c3b6905ebb2ac1c9a984cce3fb4d170'
if [[ "${_git}" == "false" ]]; then
  if [[ "${_git_service}" == "gitlab" ]]; then
    _sum="${_release_sum}"
    _sig_sum="${_release_sig_sum}"
  else
    _sum="${_release_sum}"
    _sig_sum="${_release_sig_sum}"
  fi
elif [[ "${_git}" == "true" ]]; then
  _sum="${_release_sum}"
  _sig_sum="${_release_sig_sum}"
fi
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
_sf="https://downloads.sourceforge.net"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_source}" == "sourceforge" ]]; then
      _uri="${_sf}/${_pkg}/${_tarfile}"
    else
      if [[ "${_git_service}" == "github" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/archive/${_commit}.${_archive_format}"
          _sum="${_github_sum}"
        fi
      elif [[ "${_git_service}" == "gitlab" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
        fi
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
if [[ -v "_src" ]]; then
  source+=(
    "${_src}"
  )
fi
if [[ -v "_sum" ]]; then
  sha256sums+=(
    "${_sum}"
  )
fi
if [[ "${_git}" == "false" ]]; then
  b2sums=(
    "${_release_b2_sum}"
  )
fi
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

prepare() {
  cd \
    "${_tarname}"
  # Remove include list
  # https://github.com/pypa/wheel/issues/92
  sed \
    -i \
    '/^include =/,/]/d' \
    "pyproject.toml"
}

build() {
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  local \
    _lang
  _lang="en_US.UTF-8"
  cd \
    "${_tarname}"
  # we need utf locale to valid utf8 tests
  export \
    LANG="${_lang}"
  PYTHONPATH="${PWD}/build/python/" \
  "${_py}" \
    "test/alltests.py"
}

package() {
  local \
    _cmd=() \
    _site_packages \
    _license
  _cmd=(
    "import site;"
    "print("
      "site.getsitepackages()["
        "0])"
  )
  _site_packages=$(
    "${_py}" \
      -c \
        "${_cmd[*]}")
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  if [[ "${_git}" == "false" ]]; then
    # symlink license file
    install \
      -vdm755 \
      "${pkgdir}/usr/share/licenses/${pkgname}"
    _license="${_site_packages}/${_tarname}.dist-info/COPYING.txt"
    if [[ -e "${_license}" ]]; then
      if [[ "${_os}" != "Msys" ]]; then
        ln \
          -s \
          "${_license}" \
          "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.txt"
      elif [[ "${_os}" == "Msys" ]]; then
        cp \
          "${_license}" \
          "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.txt"
      fi
    else
      echo \
        "mm"
    fi
  fi
}

# vim:set ts=2 sw=2 et:
