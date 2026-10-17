# Installation guide

## 1. Download SAI2 from SYSTEMAX

Open <https://www.systemax.jp/en/sai/devdept.html>, download the official 64-bit SAI2 ZIP, and extract it. Do not place a copy of sai2.exe in this repository. Keep the extracted SAI2 directory intact.

## 2A. Install a compatible prebuilt Wine release asset

Use this only if the GitHub Release provides an archive explicitly labelled for your host distribution/architecture. The archive generated in this working copy is for CachyOS/Arch-family x86_64 and is not a universal Linux binary.

The installer checks for an x86_64 host, an Arch-family distribution, and glibc 2.44 or newer, then runs a disposable win64-prefix/Windows-command smoke test. It refuses unsupported hosts by default. For other distributions, build from source locally instead. Do not override the platform guard for a normal installation.

    ./scripts/install-prebuilt-wine.sh ./release-assets/wine-sai2-11.20-xinput2-cachyos-x86_64.tar.xz

If downloaded from a GitHub Release, replace the path with the downloaded archive path.

## 2B. Build Wine from source

Install Wine's build dependencies for your own distribution. Consult Wine's upstream build documentation for package names, then run:

    JOBS=4 ./scripts/build-from-source.sh

The default install path is:

    ~/.local/opt/wine-sai2-11.20-xinput2

## 3. Set up SAI2 and optional shortcuts

If you built from source:

    ./scripts/install-sai2.sh --wine "$HOME/.local/opt/wine-sai2-11.20-xinput2/bin/wine" --sai2 "/absolute/path/to/sai2.exe" --shortcut both

If you installed the optional CachyOS prebuilt archive, use the bin/wine path printed by the installer; by default:

    ./scripts/install-sai2.sh --wine "$HOME/.local/opt/wine-sai2-11.20-xinput2-cachyos-x86_64/bin/wine" --sai2 "/absolute/path/to/sai2.exe" --shortcut both

Supported shortcut values: desktop, menu, both, none. The Linux "menu" shortcut creates an entry under ~/.local/share/applications/.

## 4. First user test

Open SAI2 from the chosen shortcut or run:

    "$HOME/.local/bin/sai2-wine-xinput2"

Create a test canvas, pick a pressure-sensitive brush, and test both pen movement and pressure variation. Test an erase/pen-toggle action too if your tablet has an eraser. Preserve a backup of artwork while evaluating an experimental Wine build.

## Troubleshooting

Create a local report:

    ./scripts/collect-diagnostics.sh

The report is saved on the Desktop. Inspect it before sharing. It can contain usernames, local file paths, distro/kernel details, and log excerpts.
