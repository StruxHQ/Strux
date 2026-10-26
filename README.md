# Strux

*Start structured. Make it your own.*

Strux is a flexible foundation for building embedded applications on ESP32. It gives you a clean, modular starting point with WiFi, a web UI, OTA updates, and the infrastructure to grow your project without fighting your own codebase.

It's not a framework that forces you into rigid patterns. It's a well-organized starting point that you copy, rename, and shape into whatever you're building.

<img width="1096" height="591" alt="Strux web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## Features

- Wi-Fi with access-point fallback for initial setup
- React web interface served from the ESP32
- Firmware and web UI updates over OTA
- Live logs, settings, and discoverable commands
- Optional remote access and MCP integration via [Strux Relay](https://github.com/StruxHQ/strux-relay)


## Tech Stack
Layer	Stack
Firmware	C++, ESP-IDF v6.0, FreeRTOS
Frontend	React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui
Target	Any ESP32 board that declares itself — esp32_devkit and esp32c3_supermini today, both 4 MB; flash size and partition layout are the board's, not the project's
CI/CD	GitHub Actions — builds firmware + frontend, publishes releases


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
