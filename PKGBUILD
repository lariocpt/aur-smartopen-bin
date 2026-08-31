# Maintainer: lariocpt <lariocpt.dev@gmail.com>
pkgname=smartopen-bin
_pkgname=smartopen
pkgver=0.2.0
pkgrel=1
pkgdesc="Open files, folders and URLs through configurable command menus"
arch=('x86_64' 'aarch64')
url="https://github.com/lariocpt/smartopen"
license=('MIT')
provides=("$_pkgname=$pkgver")
# `opn` on the AUR is an unrelated Go program; this package ships a file of that name,
# so it conflicts with it but does not provide it.
conflicts=("$_pkgname" "opn")
# The upstream binaries are static musl builds, so there is no libc dependency at all.
# yazi and broot are what the tool integrates with, not what it needs to run.
optdepends=('yazi: file manager whose Enter opens the menu (smartopen yazi apply)'
            'broot: tree navigator whose Enter opens the menu (smartopen broot apply)')
source_x86_64=("$pkgname-$pkgver-x86_64.tar.gz::$url/releases/download/v$pkgver/$_pkgname-x86_64-unknown-linux-musl-v$pkgver.tar.gz")
source_aarch64=("$pkgname-$pkgver-aarch64.tar.gz::$url/releases/download/v$pkgver/$_pkgname-aarch64-unknown-linux-musl-v$pkgver.tar.gz")
sha256sums_x86_64=('61bf2ec20ec548b06e7bf4becc9c90dd278f9643a8ad4d12620fff7f2aa92e08')
sha256sums_aarch64=('598a0c791595f938161e096e9b9cef544fc8b1f5bae568a68ca91d56fec9c1be')

package() {
    install -Dm0755 "$srcdir/$_pkgname" "$pkgdir/usr/bin/$_pkgname"
    install -Dm0755 "$srcdir/opn" "$pkgdir/usr/bin/opn"
    install -Dm0644 "$srcdir/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm0644 "$srcdir/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
    # Completions and the man page come from the binary itself.
    # Completions and the man page come from the binary itself — and from BOTH names.
    # `opn` is what yazi, broot and the niri keybind invoke, and each binary names itself
    # from argv[0], so `opn completions zsh` emits `#compdef opn`. Packaging only the
    # long name left anyone who types `opn` with no completions and no `man opn`.
    for _bin in "$_pkgname" opn; do
        "$srcdir/$_bin" completions bash | install -Dm0644 /dev/stdin "$pkgdir/usr/share/bash-completion/completions/$_bin"
        "$srcdir/$_bin" completions zsh  | install -Dm0644 /dev/stdin "$pkgdir/usr/share/zsh/site-functions/_$_bin"
        "$srcdir/$_bin" completions fish | install -Dm0644 /dev/stdin "$pkgdir/usr/share/fish/vendor_completions.d/$_bin.fish"
        "$srcdir/$_bin" man | install -Dm0644 /dev/stdin "$pkgdir/usr/share/man/man1/$_bin.1"
    done
}
