Zoids: Battle Legends 
[![Build Status]][actions] [![Code Progress]][progress] [![Data Progress]][progress] [![Discord Badge]][discord]
=============

<!--
Replace with your repository's URL.
-->
[Build Status]: https://github.com/onionmastori2/zoidsbldecomp/actions/workflows/build.yml/badge.svg
[actions]: https://github.com/onionmastori2/zoidsbldecomp/actions/workflows/build.yml
<!--
decomp.dev progress badges
See https://decomp.dev/api for an API overview.
-->
[Code Progress]: https://decomp.dev/onionmastori2/zoidsbldecomp.svg?mode=shield&measure=code&label=Code
[Data Progress]: https://decomp.dev/onionmastori2/zoidsbldecomp.svg?mode=shield&measure=data&label=Data
[progress]: https://decomp.dev/onionmastori2/zoidsbldecomp
<!--
Replace with your Discord server's ID and invite URL.
-->
[Discord Badge]: 
[discord]:

**HELP WANTED**: Looking for more folks to help me take on this project.

A work-in-progress decompilation of Zoids: Battle Legends.

This repository does **not** contain any game assets or assembly whatsoever. An existing copy of the game is required.

Supported versions:

- GZSE70: Rev 0 (USA)

Dependencies
============

Windows
--------

On Windows, it's **highly recommended** to use native tooling. WSL or msys2 are **not** required.  
When running under WSL, [objdiff](#diffing) is unable to get filesystem notifications for automatic rebuilds.

- Install [Python](https://www.python.org/downloads/) and add it to `%PATH%`.
  - Also available from the [Windows Store](https://apps.microsoft.com/store/detail/python-311/9NRWMJP3717K).
- Download [ninja](https://github.com/ninja-build/ninja/releases) and add it to `%PATH%`.
  - Quick install via pip: `pip install ninja`

macOS
------

- Install [ninja](https://github.com/ninja-build/ninja/wiki/Pre-built-Ninja-packages):

  ```sh
  brew install ninja
  ```

- Install [wine-crossover](https://github.com/Gcenx/homebrew-wine):

  ```sh
  brew install --cask --no-quarantine gcenx/wine/wine-crossover
  ```

After OS upgrades, if macOS complains about `Wine Crossover.app` being unverified, you can unquarantine it using:

```sh
sudo xattr -rd com.apple.quarantine '/Applications/Wine Crossover.app'
```

Linux
------

- Install [ninja](https://github.com/ninja-build/ninja/wiki/Pre-built-Ninja-packages).
- For non-x86(_64) platforms: Install wine from your package manager.
  - For x86(_64), [wibo](https://github.com/decompals/wibo), a minimal 32-bit Windows binary wrapper, will be automatically downloaded and used.

Building
========

- Clone the repository:

  ```sh
  git clone https://github.com/OnionMastori2/zoids.git
  ```

- Copy your game's disc image to `orig/GZSE70`.
  - Supported formats: ISO (GCM), RVZ, WIA, WBFS, CISO, NFS, GCZ, TGC
  - After the initial build, the disc image can be deleted to save space.

- Configure:

  ```sh
  python configure.py
  ```

  To use a version other than `GZSE70` (USA), specify it with `--version`.

- Build:

  ```sh
  ninja
  ```

Diffing
=======

Once the initial build succeeds, an `objdiff.json` should exist in the project root.

Download the latest release from [encounter/objdiff](https://github.com/encounter/objdiff). Under project settings, set `Project directory`. The configuration should be loaded automatically.

Select an object from the left sidebar to begin diffing. Changes to the project will rebuild automatically: changes to source files, headers, `configure.py`, `splits.txt` or `symbols.txt`.

![](assets/objdiff.png)
