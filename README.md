# Strux

*Start structured. Make it your own.*

**An ESP32 application template with Wi-Fi, a web interface, OTA updates, and room for your own code.**

Strux gives you a working starting point for standalone ESP32 applications. Copy the project, connect your hardware, and build your application without first implementing networking, settings, or a web interface.

<img width="1096" height="591" alt="Strux web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## Features

- Wi-Fi with access-point fallback for initial setup
- React web interface served from the ESP32
- Firmware and web UI updates over OTA
- Live logs, settings, and discoverable commands
- Optional remote access and MCP integration via [Strux Relay](https://github.com/StruxHQ/strux-relay)

Strux is intended for products with their own firmware logic and interface, rather than Home Assistant-focused devices.

## Getting started

**Supported boards:** ESP32 DevKit and ESP32-C3 SuperMini (4 MB flash).

To try it without a development environment, download `Strux-factory.bin` from [Releases](https://github.com/StruxHQ/Strux/releases) and flash it at offset `0x0` using [ESP Web Flasher](https://espressif.github.io/esptool-js/). Connect to `Strux-AP` to configure Wi-Fi.

To build from source, install [ESP-IDF v6.0+](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/) and [pnpm](https://pnpm.io/) with [Node.js 22+](https://nodejs.org/), or use the included dev container.

```bash
idf.py set-target esp32
idf.py build
idf.py -p /dev/ttyUSB0 flash monitor
```

## Project structure

Strux separates the reusable foundation, your application, and the hardware. That keeps application code independent of a particular ESP32 board and lets you improve the shared infrastructure without mixing in product-specific logic.

```text
main/
├── strux/              Framework services (Wi-Fi, OTA, settings, commands)
├── app/                Your product logic and managers
│   └── LedManager/     Example application manager
└── hardware/
    ├── boards/         Board-specific configuration and hardware instances
    ├── drivers/        Reusable peripheral drivers
    └── interfaces/     Hardware roles used by the application
frontend/               React web interface
```

The board layer owns the hardware. The application uses that hardware and registers its commands and settings with Strux; the framework itself stays independent of your application. Each layer has its own context responsible for its managers and initialization.

## Building your own application

Start with `main/app/LedManager/` as an example, add your own managers in `main/app/`, and customize `frontend/`. To support another board, add a folder under `main/hardware/boards/` with its pins, drivers, and build configuration. Most application features don't require changes to `main/strux/`.

## Example project

[Lablr](https://github.com/StruxHQ/Lablr) uses Strux to turn a USB DYMO LabelWriter into a standalone Wi-Fi label printer.

## License

No license is currently specified. All rights are reserved unless a license is added.
