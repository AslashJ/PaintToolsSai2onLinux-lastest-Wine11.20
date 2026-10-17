# Build dependencies by distribution

Wine is a large C/C++ project. The package names and optional features differ between Linux distributions, so this page is a practical starting point rather than an exhaustive, permanent list. The build script does not install system packages or run sudo.

The XInput2 development header is mandatory for this patch. Wine's configure step must detect XInput2, and the build script stops if it does not. On Arch-family systems the libxi package contains X11/extensions/XInput2.h; on Debian/Ubuntu the corresponding development package is libxi-dev.

## Debian / Ubuntu

Where the matching distro source package and build dependencies are available, prefer the distribution's Wine build-dependency list. For example, on a Debian/Ubuntu system with source repositories configured:

    sudo apt build-dep wine

For a manual starter set for the X11/XInput2 build path:

    sudo apt install build-essential gcc-mingw-w64-x86-64 autoconf bison flex gettext pkg-config       libx11-dev libxi-dev libxext-dev libxrender-dev libxrandr-dev libxcursor-dev       libxfixes-dev libxcomposite-dev libxdamage-dev libxinerama-dev libxkbcommon-dev       libxkbfile-dev libfreetype6-dev libfontconfig1-dev libgnutls28-dev libxml2-dev       libxslt1-dev libgl-dev libosmesa6-dev libunwind-dev

Depending on the distro release, Wine configure may report other optional features disabled. Install the corresponding -dev package if you need that feature.

## Fedora

Start with Fedora's Wine source package build dependencies if available:

    sudo dnf builddep wine

Also verify that the installed MinGW-w64 cross compiler and XInput2 development headers are present. Package names can vary between Fedora releases/spins.

## Arch Linux / CachyOS

A starting point for a 64-bit source build is:

    sudo pacman -S --needed base-devel mingw-w64-gcc libxi libx11 libxext libxrender       libxrandr libxcursor libxfixes libxcomposite libxdamage libxinerama       libxkbcommon libxkbfile freetype2 fontconfig gnutls libxml2 libxslt       mesa libunwind

Use the current package names from your distribution if they have changed.

## Check before compiling

The source build script checks for these tools and verifies that Wine's configure found XInput2:

- C/C++ build tools and make
- patch, tar, curl (for source download), and common shell utilities
- x86_64-w64-mingw32-gcc to build Wine's PE modules
- X11/XInput2 development files; configure must define HAVE_X11_EXTENSIONS_XINPUT2_H

After configure, the log/configuration files are in the temporary source work directory if the build fails; the consolidated build log is under ~/.cache/sai2-wine-build/build.log.

## Upstream references

- Wine build wiki: https://gitlab.winehq.org/wine/wine/-/wikis/Building-Wine
- Arch libxi package and XInput2 header list: https://archlinux.org/packages/extra/x86_64/libxi/
- Wine 11.20 source archive: https://dl.winehq.org/wine/source/11.x/wine-11.20.tar.xz
