# 360io

360io is a Gamescope-native console environment for CachyOS. Its Qt Quick
shell is intended to replace KDE Plasma in the dedicated session while Linux
services such as NetworkManager, PipeWire and the graphics drivers continue to
run underneath it.

The project is being rebuilt in small, verifiable stages. The current Stage 1
contains only:

- a hardware-accelerated Qt 6/QML shell with no WebEngine or Chromium;
- the 1600x900 Sign-In screen and keyboard navigation;
- a `QAbstractListModel` that discovers real Linux accounts under `/home`;
- local avatar discovery with the bundled classic avatar as a fallback;
- the final `Create Profile` action, currently exposed as a safe request;
- an unprivileged `360iod` daemon skeleton for later system coordination.

## Build on CachyOS

```sh
sudo pacman -S --needed base-devel cmake gamescope ninja \
  qt6-base qt6-declarative
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

Run the shell inside Gamescope:

```sh
gamescope -f -r 60 -w 1600 -h 900 -W 1600 -H 900 -- ./build/360io-shell
```

`QT_QPA_PLATFORM=wayland` is selected by the shell before Qt starts. The
dedicated session command is available at `packaging/arch/360io-session`.

## Profile mapping

Every directory in `/home` becomes one Sign-In profile. Avatar lookup is local
and ordered as follows:

1. `~/.face` or `~/.face.icon`;
2. `~/.config/360io/avatar.png` or `avatar.jpg`;
3. a matching file in `assets/dashx360/Profile/Profiles/`;
4. `assets/dashx360/Profile/profilepicture.jpg`.

The full-body Sign-In avatar is a live Qt Quick 3D scene, independent from the
square gamer picture. The avatar editor will generate a standardized glTF 2.0
binary model at `~/.local/share/360io/avatar/avatar.glb`. The Sign-In scene
loads that model directly, preserves its rig and animations, and displays a
neutral procedural 3D mannequin while the profile has no generated model.

For isolated tests, `THREESIXTY_HOME_ROOT` and `THREESIXTY_ASSET_ROOT` can
point the model at temporary directories. Creating an operating-system account
will later be performed by an authenticated helper; the graphical shell never
runs user-management commands as root.
