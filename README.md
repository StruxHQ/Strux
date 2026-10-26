# Strux

*Start structured. Make it your own.*

**An ESP32 application template with Wi-Fi, a web interface, OTA updates, and a clean place for your own code.**

Strux is a starting point for standalone ESP32 products in C++ and ESP-IDF. Networking, settings, updates, and a browser interface are already there, so you can focus on your device. Copy the template, rename it, and make it yours.

<img width="1096" height="591" alt="Strux web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## What's included

- **Wi-Fi** — Station mode with `Strux-AP` fallback for setup
- **Web UI** — React and TypeScript interface served directly from flash
- **OTA** — Firmware and bundled web UI updated together
- **Live console** — Browser-based logs over WebSocket
- **Settings** — Typed NVS settings with automatically generated UI controls
- **Commands** — Discoverable commands accessible over local WebSocket
- **Optional remote access** — [Strux Relay](https://github.com/StruxHQ/strux-relay), including MCP access for AI clients
- **Time sync** — SNTP and timezone support

Strux is for devices with their own logic and UI. For Home Assistant-centric devices, [ESPHome](https://esphome.io/) may be a better fit.

## Getting started

The included boards are `esp32_devkit` (ESP32 DevKit, default) and `esp32c3_supermini` (ESP32-C3 SuperMini), both with 4 MB flash.

**Flash a release:** Download `Strux-factory.bin` from [Releases](https://github.com/StruxHQ/Strux/releases), open [ESP Web Flasher](https://espressif.github.io/esptool-js/) in Chrome or Edge, select your serial port, and flash at offset `0x0`. Connect to `Strux-AP` to set up Wi-Fi.

**Build from source:** Install [ESP-IDF v6.0+](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/), [Node.js 22+](https://nodejs.org/), and [pnpm](https://pnpm.io/), or use the included dev container.

```bash
idf.py set-target esp32
idf.py build
idf.py -p /dev/ttyUSB0 flash monitor
```

With pnpm installed, the frontend is built and bundled into the firmware automatically.

## Make it yours

| Location | Purpose |
| --- | --- |
| `main/app/` | Your application logic, managers, and commands |
| `main/hardware/boards/` | Board configurations and hardware instances |
| `main/hardware/drivers/` | Reusable peripheral drivers |
| `main/strux/` | Shared networking, settings, OTA, and command infrastructure |
| `frontend/` | React web interface |

Start with `main/app/LedManager/` as a working example. Add your application managers in `main/app/`, configure hardware in `main/hardware/`, and customize the frontend. Most applications do not need changes to `main/strux/`.

To add a board, copy an existing folder in `main/hardware/boards/` and adapt its pin definitions, board context, build configuration, and partition layout. Build with `idf.py -DBOARD=<your_board> set-target <chip>` followed by `idf.py -DBOARD=<your_board> build`.

## Built with Strux

[Lablr](https://github.com/StruxHQ/Lablr) turns a USB DYMO LabelWriter into a standalone Wi-Fi label printer using an ESP32-S3.

## Tech stack

| Layer | Technology |
| --- | --- |
| Firmware | C++, ESP-IDF v6.0, FreeRTOS |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| CI/CD | GitHub Actions for builds and releases |

## License

No license is currently specified. All rights are reserved unless a license is added.
