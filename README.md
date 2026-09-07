# MINIHAT

MINIHAT is an STM32H747-based development board that combines wired
communication, display, audio, removable storage, and wireless connectivity
interfaces on one compact platform.

The project contains both the KiCad hardware design and the STM32CubeMX/CMake
firmware project. It is currently under development; the status of individual
interfaces is listed below.

## Features and status

| Interface or subsystem | Description | Hardware | Firmware | MCU peripheral |
| --- | --- | :---: | :---: | --- |
| CAN | CAN frame reception and transmission | **K** | **V** | FDCAN |
| Ethernet | 10/100 Ethernet through the LAN8720 PHY | **V** | **V** | Ethernet MAC |
| USB | USB connection to a host computer | **V** | **K** | USB |
| Display | Basic information display through LTDC/HDMI | **K** | **K** | LTDC, DSI host |
| Bluetooth | Wireless connection and audio reception; antenna not included yet | **K** | **K** | USART2 |
| Audio output | Digital audio output for an external amplifier or speaker | **V** | **K** | SAI |
| Debug | Debug and diagnostic serial interface | **K** | **K** | USART1 |
| QSPI flash | W25-series flash for graphics and other assets | **V** | **V** | QUADSPI |
| SD card | Removable storage connector | **V** | **V** | SDMMC |
| Power | USB-C supply | Proposed | - | - |

## Functional description

MINIHAT is intended to serve as a central controller and communication hub for
embedded systems. The main functional blocks are:

- **STM32H747 MCU:** The dual-core microcontroller runs the application and
  handles communication with all peripherals. The Cortex-M7 core is intended
  for the main application, networking, graphics, and other high-performance
  tasks, while the Cortex-M4 core can handle supporting or time-sensitive
  functions independently.
- **CAN:** The interface supports receiving and transmitting CAN frames from BMW MINI car.
- **Ethernet with LAN8720:** Connects the board to a wired local network. It
  is used for board configuration, diagnostics, acquisition od data from car on host device.
- **USB:** Provides a direct connection to a computer for host device/host app.
- **Display output:** The LTDC display path is intended to show basic status
  information, bios menu. The planned HDMI  bridge allows connection to a compatible external display.
- **Bluetooth:** Provides a short-range wireless link to a phone or another
  host, which uses host app providing reads of basic system parameters, and sending audio data to play. The planned use includes receiving control data and audio streams.
- **Audio output:** The SAI interface transfers digital audio samples so that received  
  or generated audio can be played through speakers.
- **Debug interface:** The serial debug connection is used for boot messages,
  diagnostics, development logging, and low-level troubleshooting, for debug stage of project.
- **QSPI flash:** Stores graphics, configuration data, firmware assets, and
  other files that require non-volatile memory with faster access than an SD
  card.
- **SD card:** Provides removable mass storage for logs, media, configuration
  files, and data exchange with a computer.

<span style="color: gray">- **Dual-core firmware:** The firmware project is generated from STM32CubeMX  and built as separate CM7 and CM4 targets. Shared startup code coordinates  the two cores and the generated HAL/driver layers provide access to the MCU peripherals.</span>

## Main hardware

- **MCU:** STM32H747IGT6 (dual-core Cortex-M7/Cortex-M4)
- **Ethernet PHY:** LAN8720
- **External memory:** W25-series QSPI flash and SD card
- **Audio:** SAI interface routed to an external audio device
- **Display:** LTDC display interface with a planned HDMI bridge
- **PCB design:** KiCad

The current high-level design is shown below:

![MINIHAT block diagram](schemat_ideowy.drawio.svg)

## Repository layout

```text
.
├── FIRMWARE/
│   └── MNI_HAT_V0/
│       ├── CM7/                 # Cortex-M7 target and linker scripts
│       ├── CM4/                 # Cortex-M4 target and linker scripts
│       ├── Common/              # Shared dual-core startup code
│       └── Drivers/             # CMSIS and STM32 device drivers
├── HARDWARE/
│   └── MINIHATv.0/              # KiCad schematics, PCB, and libraries
├── schemat_ideowy.drawio.svg    # High-level block diagram
└── README.md
```

## Firmware build

### Requirements

- CMake 3.22 or newer
- Ninja
- `arm-none-eabi-gcc` toolchain
- A programmer/debugger compatible with the STM32H747

The firmware uses CMake presets and separate build directories for each core.
From the repository root, configure and build the desired target:

```powershell
# Cortex-M7
cmake --preset Debug -S FIRMWARE/MNI_HAT_V0/CM7
cmake --build FIRMWARE/MNI_HAT_V0/CM7/build/Debug

# Cortex-M4
cmake --preset Debug -S FIRMWARE/MNI_HAT_V0/CM4
cmake --build FIRMWARE/MNI_HAT_V0/CM4/build/Debug
```

Available presets are `Debug`, `Release`.
Build the CM7 and CM4 images separately and use the linker scripts in the
corresponding target directory when programming the device.

The generated firmware is based on STM32CubeMX. When changing the `.ioc`
configuration, regenerate the project and review generated changes before
building.

## Hardware

Open `HARDWARE/MINIHATv.0/MINIHATv.0.kicad_pro` with KiCad to inspect the
complete design. Functional blocks are also kept as separate schematics:

- `MCU.kicad_sch`
- `CAN.kicad_sch`
- `Ethernet.kicad_sch`
- `usb.kicad_sch`
- `Bluetooth.kicad_sch`
- `audio.kicad_sch`
- `HDMI.kicad_sch`
- `QSPI.kicad_sch`
- `sdcarad.kicad_sch`
- `sdram.kicad_sch`
