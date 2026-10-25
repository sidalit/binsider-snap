<div align="center">

<img src="snap/gui/binsider.png" alt="Binsider logo" width="128" />

# Binsider

**Inspect ELF binaries from your terminal.**

[![binsider](https://snapcraft.io/binsider/badge.svg)](https://snapcraft.io/binsider)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Binsider](https://github.com/orhun/binsider), a terminal interface for inspecting headers, symbols, strings and hexadecimal data.

</div>

---

## Getting Started

<a href="https://snapcraft.io/binsider"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install binsider
cp /usr/bin/ls ~/ls
binsider ~/ls
```

Copy host binaries into your home folder before opening them. Binsider can inspect visible files there without additional setup.

## Configure

There are no `snap set` options. Choose the view with command-line options, such as `binsider --tab strings --min-len 8 ~/ls`; see `binsider --help` for the available options.

To open files on removable drives under `/media` or `/mnt`:

```bash
sudo snap connect binsider:removable-media
```

## Limitations

- System call tracing is disabled. The Dynamic tab reports that the feature is unavailable; static inspection still works. Use your host's `strace` separately when you need tracing.
- `/usr/bin` and `/usr/lib` refer to the snap's base, so their binaries and libraries may differ from your host's.
- Host paths such as `/usr/local`, `/opt` and `/tmp` are not visible. Copy the binary into a visible folder in your home directory first.

## Build

```bash
git clone https://github.com/sidalit/binsider-snap.git
cd binsider-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/binsider-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/orhun/binsider/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/binsider-snap/blob/main/LICENSE).
