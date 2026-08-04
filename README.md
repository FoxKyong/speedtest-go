# speedtest-go (Arch Linux PKGBUILD)

Arch Linux `PKGBUILD` that builds **speedtest-go**, a CLI and Go API to test
internet speed using speedtest.net
([showwin/speedtest-go](https://github.com/showwin/speedtest-go)).

This is a continuation of the
[AUR `speedtest-go`](https://aur.archlinux.org/packages/speedtest-go)
package, kept up to date with newer upstream releases. Full credit for the
original packaging goes to the maintainer listed in the `PKGBUILD` header; this
repo only tracks new upstream versions on top of that work.

## What you get

- `speedtest-go` — the CLI client, installed to `/usr/bin/speedtest-go`

Built from the upstream release tarball with `CGO_*` flags and `-buildmode=pie
-trimpath` per Arch Go packaging guidelines.

## Building & installing

```bash
git clone https://github.com/FoxKyong/speedtest-go.git
cd speedtest-go
makepkg -si
```

`go` is the only build dependency.

Note that `check()` runs the upstream test suite (`go test ./speedtest`), which
talks to speedtest.net and therefore **needs a working internet connection**.
Use `makepkg --nocheck` to skip it.

## Updating to a new version

Upstream tags every release on GitHub, so the latest version is whatever
[`releases/latest`](https://github.com/showwin/speedtest-go/releases/latest)
points at. To bump:

1. Set `pkgver` to the new version.
2. Regenerate the checksum: `makepkg -g` and paste the printed `sha256sums=(...)`.
3. Regenerate metadata: `makepkg --printsrcinfo > .SRCINFO`.
4. Verify it builds: `makepkg -f`.

The built binary reports its version as
`speedtest-go v<version> git-dev built at unknown` — the `git-dev` and
`unknown` parts are expected for a tarball build, since the upstream build
stamps those in from git metadata that a release tarball does not carry.

## License

speedtest-go is licensed under the **MIT** license (see `LICENSE` in the
upstream repository). This repository contains only the packaging recipe; the
source code is downloaded from GitHub during the build.
