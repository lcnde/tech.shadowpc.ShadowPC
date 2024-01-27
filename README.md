# Build-commands
```yaml
- cp /usr/bin/ar /app/bin
- cp /usr/lib/x86_64-linux-gnu/libsframe.so.1 /app/lib
```
These 2 commands are necessary otherwise the script inside sources would not be able to unpack the `.deb` file. The first one is the `ar` gnu utility, it is part of the `binutils` utilities. It is already installed on most linux systems, in fact the flatpak build commands are copying it from the host linux system, and transfers it inside flatpak environment.
The second `cp` command is a library that is necessary for the `ar` command to work.

To find the location for the libsframe.so.1 library, you can use
```
$ apt-file search libsframe.so.1
```

# Obsolete code
```
  # - name: binutils
  #   buildsystem: autotools
  #   sources:
  #     - type: archive
  #       url: "https://ftp.gnu.org/gnu/binutils/binutils-2.36.1.tar.gz"
  #       sha256: "e68edeaaeb6ca9687b6dcbaedd1b376506baad2d48de26a885fc5ab6acb839da"
  # - name: host-spawn
  #   buildsystem: simple
  #   build-commands:
  #     - install -Dm755 host-spawn /app/bin/host-spawn
  #   sources:
  #     - type: file
  #       url: https://github.com/1player/host-spawn/releases/download/1.5.0/host-spawn-x86_64
  #       sha256: dbf67e7e111c4fe1edb0c642cbb4193064ca5b384aeb1054fc2befba6ed88b83
  #       dest-filename: host-spawn
  #       only-arches: [x86_64]
  #     - type: file
  #       url: https://github.com/1player/host-spawn/releases/download/1.5.0/host-spawn-aarch64
  #       sha256: c42c12be6cdd83e374b847bec836659fb45231215797777c9ee1c9c0ae9e3783
  #       dest-filename: host-spawn
  #       only-arches: [aarch64]
```