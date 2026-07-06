# 360io

360io is a Gamescope-native console environment for Linux focused on recreating
the complete Xbox 360 console experience on modern hardware. It replaces the
traditional desktop with a controller-first shell while Linux services such as
NetworkManager, PipeWire and the graphics stack continue running underneath.

The project combines a native Qt 6/QML interface with modern Linux gaming
technologies to provide a dedicated console operating environment designed for
controllers, fast boot, and seamless game launching.

## Planned features

The long-term goal of 360io includes:

- a fully hardware-accelerated Qt Quick shell running directly inside Gamescope;
- a dashboard experience inspired by the Xbox 360 user interface;
- Sign-In, Guide, Profile and System blades;
- local profiles with customizable gamer pictures and 3D avatars;
- native avatar rendering using Qt Quick 3D and glTF 2.0 assets;
- controller-first navigation throughout the entire operating system;
- integrated game library supporting native Linux games, Steam, Xenia and
  additional gaming platforms;
- achievement integration with profile progression and avatar customization;
- optional Kinect support;
- optional optical drive support;
- dedicated boot and shutdown experience;
- fast, appliance-like startup with no traditional desktop session.

## Architecture

360io consists of several independent components:

- **360io Shell** — the graphical Qt Quick interface.
- **360iod** — an unprivileged background daemon responsible for system
  coordination.
- **Avatar Engine** — avatar rendering, asset management and model conversion.
- **Profile Manager** — local user discovery and profile management.
- **Game Library** — launcher integration and library indexing.
- **System Services** — session management, updates and hardware integration.

## Current status

Development is progressing through small, verifiable milestones.

Current progress includes:

- hardware-accelerated Qt 6/QML shell;
- Gamescope-native execution;
- Sign-In screen;
- controller keyboard navigation;
- Linux user discovery;
- local avatar discovery;
- Qt Quick 3D avatar rendering;
- avatar model parser and conversion research;
- unprivileged 360iod daemon foundation.

Additional dashboard components, avatar editing, Guide functionality,
achievement integration and hardware support are currently under active
development.

## Design goals

360io is designed around the following principles:

- controller-first interaction;
- native Linux technologies;
- no Chromium or embedded web interfaces;
- modular architecture;
- modern hardware support;
- console-like responsiveness;
- faithful recreation of the Xbox 360 user experience.

## Build

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

## License

See the LICENSE file for licensing information.
