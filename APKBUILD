pkgname=skopeo
pkgver=1.16.1
pkgrel=0
# set this to the gitrev of the version
_gitrev=fe07cc958acae9bb520f685474a50178e00b815b
pkgdesc="Work with remote images registries - retrieving information, images, signing content"
url="https://github.com/containers/skopeo"
license="Apache-2.0"
arch="all"
options="net !check" # needs docker
depends="containers-common"
makedepends="
	bash
	btrfs-progs-dev
	glib-dev
	go
	go-md2man
	gpgme-dev
	libselinux-dev
	linux-headers
	lvm2-dev
	ostree-dev
	"
subpackages="
	$pkgname-doc
	$pkgname-bash-completion
	$pkgname-fish-completion
	$pkgname-zsh-completion
	"
source="https://github.com/kostya253/skopeo/releases/download/v1.16.1/skopeo-1.16.1.tar.gz"

export GOCACHE="${GOCACHE:-"$srcdir/go-cache"}"
export GOTMPDIR="${GOTMPDIR:-"$srcdir"}"
export GOMODCACHE="${GOMODCACHE:-"$srcdir/go"}"

build() {
	# https://github.com/mattn/go-sqlite3/issues/1164
	export CGO_CFLAGS="$CFLAGS -D_LARGEFILE64_SOURCE"

	make GIT_COMMIT=$_gitrev all
}

check() {
	make check
}

package() {
	make DESTDIR="$pkgdir" PREFIX=/usr install-docs install-completions
	install -Dm755 bin/skopeo -t "$pkgdir"/usr/bin/
}



sha512sums="
06e6b965f27876d0bc6d0a45cacb00c0b4e4ba0abba090315fdfef39d8ff72217ad0b6cc4cbdb9d5bb5754ffad270c02aae9f553db775afa17a9764d1f8d691d  skopeo-1.16.1.tar.gz
"
