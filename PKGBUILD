# Maintainer: lariocpt <lariocpt.dev@gmail.com>
pkgname=smartopen-bin
_pkgname=smartopen
pkgver=0.2.0
pkgrel=1
pkgdesc="Open files, folders and URLs through configurable command menus — from yazi, broot, your shell or a keystroke"
arch=('x86_64' 'aarch64')
url="https://github.com/lariocpt/smartopen"
license=('MIT')
provides=("$_pkgname=$pkgver" "opn")
conflicts=("$_pkgname" "opn")
# The upstream binaries are static musl builds, so there is no libc dependency at all.
# yazi and broot are what the tool integrates with, not what it needs to run.
optdepends=('yazi: file manager whose Enter opens the menu (smartopen yazi apply)'
            'broot: tree navigator whose Enter opens the menu (smartopen broot apply)')
source_x86_64=("$pkgname-$pkgver-x86_64.tar.gz::$url/releases/download/v$pkgver/$_pkgname-x86_64-unknown-linux-musl-v$pkgver.tar.gz")
source_aarch64=("$pkgname-$pkgver-aarch64.tar.gz::$url/releases/download/v$pkgver/$_pkgname-aarch64-unknown-linux-musl-v$pkgver.tar.gz")
sha256sums_x86_64=('REPLACE_WITH_SHA256SUMS_ENTRY')
sha256sums_aarch64=('REPLACE_WITH_SHA256SUMS_ENTRY')

package() {
    install -Dm0755 "$srcdir/$_pkgname" "$pkgdir/usr/bin/$_pkgname"
    install -Dm0755 "$srcdir/opn" "$pkgdir/usr/bin/opn"
    install -Dm0644 "$srcdir/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm0644 "$srcdir/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
    # Completions and the man page come from the binary itself.
    "$srcdir/$_pkgname" completions bash | install -Dm0644 /dev/stdin "$pkgdir/usr/share/bash-completion/completions/$_pkgname"
    "$srcdir/$_pkgname" completions zsh  | install -Dm0644 /dev/stdin "$pkgdir/usr/share/zsh/site-functions/_$_pkgname"
    "$srcdir/$_pkgname" completions fish | install -Dm0644 /dev/stdin "$pkgdir/usr/share/fish/vendor_completions.d/$_pkgname.fish"
    "$srcdir/$_pkgname" man | install -Dm0644 /dev/stdin "$pkgdir/usr/share/man/man1/$_pkgname.1"
}
