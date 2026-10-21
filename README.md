# Binsider snap

[![binsider](https://snapcraft.io/binsider/badge.svg)](https://snapcraft.io/binsider)

Snap packaging for [Binsider](https://github.com/orhun/binsider), a terminal interface for ELF inspection, hexadecimal analysis, and static/dynamic binary analysis.

Unofficial build, not affiliated with or endorsed by the Binsider project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/binsider"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install binsider                   # or a local build: ./binsider_0.3.2_*.snap --dangerous
sudo snap connect binsider:removable-media   # optional: /media, /mnt
cp /usr/bin/ls ~/ls
binsider ~/ls
binsider --tab strings --min-len 8 ~/ls
```

## Known limitations

### Dynamic analysis

The snap is built without system call tracing. The Dynamic tab is still there, but it only shows a message saying the `dynamic-analysis` feature is not enabled. Tracing needs the `ptrace` system call, which strict confinement blocks, and no interface a normal snap can use allows it.

To trace a program, use `strace` on your system or the upstream `binsider` binary:

```bash
strace -f ./my-program
```

### System binaries

Binsider runs inside the snap sandbox, so `/usr/bin` and `/usr/lib` are those of the snap's base (Ubuntu Core 26), not of your system. `binsider /usr/bin/ls` opens the base's `ls`, and the shared libraries listed in the General tab come from the base too.

Paths that only exist on your system, such as `/usr/local`, `/opt` or `/tmp`, are not visible and fail with `Unable to locate binary`. To inspect such a file, copy it to your home directory first:

```bash
cp /usr/local/bin/my-program ~/
binsider ~/my-program
```

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Binsider is licensed under MIT or Apache-2.0; its dependencies carry their own licenses.
