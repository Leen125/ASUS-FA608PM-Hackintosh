# ASUS FA608PM Hackintosh

> OpenCore EFI configuration, hardware compatibility notes, and macOS
> experimentation for the ASUS TUF Gaming A16 FA608PM.

**Project status:** `Experimental` · For research and testing only.

[简体中文](README_CN.md) \| **English**

------------------------------------------------------------------------

## Table of Contents

-   [Overview](#overview)
-   [Project Scope](#project-scope)
-   [Hardware Specifications](#hardware-specifications)
-   [Compatibility Status](#compatibility-status)
-   [Known Issues](#known-issues)
-   [NVIDIA Graphics and NullMoth
    Driver](#nvidia-graphics-and-nullmoth-driver)
-   [Repository Structure](#repository-structure)
-   [Before You Begin](#before-you-begin)
-   [Installation Workflow](#installation-workflow)
-   [EFI and Configuration Notes](#efi-and-configuration-notes)
-   [Hardware Validation Plan](#hardware-validation-plan)
-   [Troubleshooting](#troubleshooting)
-   [Testing Other ASUS TUF AMD
    Laptops](#testing-other-asus-tuf-amd-laptops)
-   [Privacy and Security](#privacy-and-security)
-   [Contributing](#contributing)
-   [Licensing](#licensing)
-   [Disclaimer](#disclaimer)
-   [Acknowledgements](#acknowledgements)

------------------------------------------------------------------------

## Overview

This repository documents ongoing Hackintosh research on the **ASUS TUF
Gaming A16 FA608PM**. It is intended to record the tested configuration,
hardware compatibility, OpenCore-related notes, known limitations, and
reproducible test results.

The project prioritizes transparent documentation over claims of
complete compatibility. A successful boot does **not** mean every device
or macOS feature works.

## Project Scope

The project aims to:

-   Document the test machine and its current macOS configuration.
-   Track working, non-working, and untested hardware features.
-   Keep configuration changes and troubleshooting findings
    understandable.
-   Publish installation notes and reproducible test procedures as they
    are verified.
-   Investigate third-party graphics-driver research without overstating
    its capabilities.
-   Explore other ASUS TUF laptops with AMD processors only when their
    exact hardware has been independently tested.

This repository is not a universal EFI. Hardware revisions, BIOS
settings, firmware, and component substitutions can change
compatibility.

## Hardware Specifications

  -----------------------------------------------------------------------
  Component                           Current test machine
  ----------------------------------- -----------------------------------
  Laptop                              ASUS TUF Gaming A16 FA608PM

  CPU                                 AMD Ryzen 9 8940HX

  Dedicated GPU                       NVIDIA GeForce RTX 5060 Laptop GPU,
                                      8 GB GDDR7

  Operating system                    macOS Tahoe 26.7.2

  Wi-Fi                               Realtek RTL8852CE

  Bluetooth                           Realtek USB Bluetooth, VID:PID
                                      `0489:E122`

  Bootloader                          OpenCore (record the exact version
                                      used for each release)
  -----------------------------------------------------------------------

BIOS version, memory configuration, storage model, audio codec, OpenCore
version, and exact kext versions should be added to the test record when
confirmed. Do not guess missing specifications.

## Compatibility Status

The table below describes the current test machine only. Status may
change as new tests are performed.

  -----------------------------------------------------------------------
  Feature                 Status                  Notes
  ----------------------- ----------------------- -----------------------
  macOS boot              ✅ Working              Boots the documented
                                                  test installation

  Wi-Fi                   ✅ Working              Realtek RTL8852CE
                                                  reported working in the
                                                  current setup

  Audio                   ✅ Working              Working configuration
                                                  was recovered by
                                                  comparing the old and
                                                  new EFI
                                                  `DeviceProperties`

  Bluetooth               ❌ Not working          Realtek USB device
                                                  `0489:E122`; further
                                                  investigation required

  Display brightness      ❌ Not working          Brightness adjustment
  control                                         is currently
                                                  unavailable

  NVIDIA graphics         ⚠️ Not confirmed        Driver research is
  acceleration                                    ongoing; full
                                                  acceleration and Metal
                                                  support must not be
                                                  assumed

  Sleep and wake          ⏳ Not tested           No verified result
                                                  recorded

  External displays       ⏳ Not tested           No verified result
                                                  recorded

  Microphone and audio    ⏳ Not separately       Verify input devices
  input                   tested                  independently

  USB port mapping        ⏳ Not fully documented Test each port and its
                                                  speed

  Battery, power          ⏳ Not fully tested     Record behavior under
  management, and                                 repeatable conditions
  thermals                                        

  Camera, keyboard        ⏳ Not fully tested     Validate individually
  shortcuts, and function                         
  keys                                            
  -----------------------------------------------------------------------

**Status definitions**

-   `Working`: tested on this machine and currently functional.
-   `Not working`: tested and currently known to fail.
-   `Under investigation`: some work has been attempted, but the result
    is not sufficiently verified.
-   `Not tested`: no reliable test result is available.

Do not treat an untested feature as working.

## Known Issues

### Bluetooth

The current Realtek USB Bluetooth device (`VID:PID 0489:E122`) is not
working in the documented macOS setup. No fix is claimed here. Record
relevant USB enumeration, logs, and any tested configuration changes
before reporting a solution.

### Display brightness

Display brightness control is not working. This may involve
platform-specific ACPI, display-panel control, or other
hardware/firmware behavior. Do not apply random ACPI patches without
understanding their effect and backing up the current EFI.

### NVIDIA GPU

The presence of a third-party driver does not establish that the RTX
5060 Laptop GPU is fully supported. Graphics acceleration, Metal,
display output, sleep behavior, and application compatibility require
separate verification.

### Audio configuration

Audio currently works. During troubleshooting, the known-working audio
`DeviceProperties` from the previous EFI were copied into the newer EFI,
restoring audio. If audio breaks after an EFI change, compare the
known-working configuration first rather than repeatedly changing
unrelated settings. Remove personal identifiers before sharing
configuration files.

## NVIDIA Graphics and NullMoth Driver

This project investigates the third-party [NullMoth NVIDIA macOS
Driver](https://github.com/nullmoth/nvidia-macos-driver).

The driver is an external project and is not developed or maintained by
this repository. Compatibility with this laptop, the RTX 5060 Laptop
GPU, the current macOS version, graphics acceleration, Metal, and
individual applications must be established by actual tests.

When documenting results, include:

-   Exact macOS version and build, where available.
-   Exact driver release or commit used.
-   Installation and boot conditions.
-   Test method, expected result, and observed result.
-   Relevant logs with personal identifiers removed.
-   Any regressions, instability, or limitations.

Do not describe the GPU as fully accelerated or Metal-compatible unless
reproducible tests demonstrate that result.

## Repository Structure

The repository can grow into the following structure as files are added:

    ASUS-FA608PM-Hackintosh/
    ├── README.md
    ├── README_CN.md
    ├── LICENSE
    ├── docs/
    │   ├── INSTALLATION.md
    │   ├── CONFIGURATION.md
    │   ├── COMPATIBILITY.md
    │   └── TROUBLESHOOTING.md
    ├── configs/
    │   └── README.md
    └── tests/
        └── README.md

  -----------------------------------------------------------------------
  Path                                Purpose
  ----------------------------------- -----------------------------------
  `README.md`                         Main English project overview

  `README_CN.md`                      Main Simplified Chinese project
                                      overview

  `LICENSE`                           License for original repository
                                      content, once selected

  `docs/`                             Detailed installation,
                                      configuration, compatibility, and
                                      troubleshooting guides

  `configs/`                          Sanitized, documented configuration
                                      examples, if published

  `tests/`                            Test plans and results
  -----------------------------------------------------------------------

Only include directories and files that actually exist in the
repository, or clearly label them as planned. Never publish personal EFI
data or machine-specific identifiers accidentally.

## Before You Begin

> \[!WARNING\] Hackintosh installation and EFI changes can make a system
> unbootable or cause data loss. Proceed only if you understand the
> risks.

Before attempting any changes:

1.  Back up important files and create a recovery plan.
2.  Keep a separate copy of the currently working EFI.
3.  Confirm that you can access your firmware setup and recovery media.
4.  Record the exact BIOS, macOS, OpenCore, and kext versions.
5.  Read the license and documentation of every third-party component.
6.  Make one change at a time and record the result.
7.  Do not use an EFI intended for a different laptop without reviewing
    every relevant hardware difference.

This repository is a research record, not a guarantee that the
configuration will work on another machine.

## Installation Workflow

A detailed, verified installation guide should be maintained in
`docs/INSTALLATION.md`. Until that guide is complete and tested end to
end, use the following as a high-level workflow rather than a promise of
compatibility:

1.  **Check the hardware.** Confirm the exact laptop model and hardware
    revision.
2.  **Prepare recovery options.** Back up data and preserve a known-good
    EFI.
3.  **Review the configuration.** Understand the OpenCore version, ACPI
    files, kexts, drivers, and configuration settings being used.
4.  **Review third-party requirements.** Follow the upstream
    documentation and licenses for all external drivers and tools.
5.  **Validate configuration files.** Use documentation appropriate to
    the exact OpenCore version. Do not copy settings blindly between
    versions.
6.  **Boot and test carefully.** Record the boot result and test
    hardware features individually.
7.  **Document failures.** Save sanitized logs and note the last change
    made.
8.  **Update the compatibility table.** Only mark a feature working
    after testing it on the target machine.

No installer, EFI archive, or third-party driver should be assumed to be
included unless it is explicitly present in the repository.

## EFI and Configuration Notes

OpenCore configurations are hardware- and version-sensitive. Keep
changes traceable and document the purpose of each modification.

Areas that may require documentation include:

-   `ACPI`: tables and patches used by the configuration.
-   `Booter` and `Kernel`: boot behavior and kernel-related settings.
-   `DeviceProperties`: device-specific properties, including the
    known-working audio configuration.
-   `NVRAM`: boot arguments and stored variables.
-   `UEFI`: firmware drivers and boot settings.
-   `Kernel -> Add`: kexts, their versions, dependencies, and sources.
-   `Misc`: OpenCore tools, security settings, and boot-picker behavior.

The list is a documentation guide, not a claim that every item has been
fully configured or verified in this repository.

**Important:** Never publish a personal `SystemSerialNumber`, `MLB`,
`SystemUUID`, or other identifying values. Sanitize `config.plist`,
logs, screenshots, and EFI archives before sharing them. Keep a private
backup of the original configuration.

## Hardware Validation Plan

Use a repeatable checklist and update the compatibility table only after
recording results.

  -----------------------------------------------------------------------
  Test area                           Suggested validation
  ----------------------------------- -----------------------------------
  Boot stability                      Cold boot, restart, and repeated
                                      boot attempts

  Wi-Fi                               Connect, reconnect, test sustained
                                      traffic, and test after sleep if
                                      sleep works

  Bluetooth                           Confirm device enumeration,
                                      pairing, connection stability, and
                                      reconnection

  Audio output                        Test speakers and headphone output
                                      at several volume levels

  Audio input                         Test microphone selection and
                                      recording

  Brightness                          Test all available brightness
                                      controls and persistence after
                                      reboot

  Sleep and wake                      Test sleep, wake, display
                                      restoration, network recovery, and
                                      input devices

  USB                                 Test every port, data transfer, and
                                      device reconnect behavior

  External display                    Test each available output and
                                      supported display mode

  Graphics                            Record driver version, acceleration
                                      evidence, Metal status, and
                                      application behavior separately

  Power and thermals                  Observe battery reporting, idle
                                      behavior, temperatures, and
                                      sustained load

  Keyboard and camera                 Test individual keys, function
                                      shortcuts, and camera availability
  -----------------------------------------------------------------------

For each test, record date, software versions, steps, expected behavior,
actual behavior, and logs. Avoid drawing broad conclusions from a single
successful boot.

## Troubleshooting

### General procedure

1.  Identify the last change made.
2.  Reproduce the issue with a consistent sequence of steps.
3.  Compare against the last known-working configuration.
4.  Change one variable at a time.
5.  Keep logs and remove personal identifiers before sharing.
6.  If a change makes the system worse, restore the backup before trying
    another approach.

### Audio stopped working after an EFI change

The previously working audio configuration was restored by copying the
relevant `DeviceProperties` from the older EFI into the newer EFI.
Compare that known-working section first. Do not overwrite the entire
new configuration blindly; compare the relevant keys and preserve a
backup.

### Bluetooth is unavailable

Confirm that the USB Bluetooth device is detected, record its VID:PID
(`0489:E122`), and collect sanitized logs. Do not claim a fix unless the
device is tested through pairing, connection, and reconnection.

### Brightness controls do not work

Record the panel and platform behavior, available brightness controls,
and any relevant logs. Avoid unverified ACPI changes and keep a
recoverable EFI.

### Boot or configuration failures

Check that the configuration matches the OpenCore version and the target
machine. Review changes, firmware settings, and sanitized logs. Do not
assume a configuration from another model is interchangeable.

## Testing Other ASUS TUF AMD Laptops

The primary target of this repository is the **ASUS TUF Gaming A16
FA608PM**. Other ASUS TUF laptops with AMD processors may be
investigated in the future, but they must be treated as separate test
targets.

Different CPU generations, GPUs, Wi-Fi and Bluetooth modules, audio
devices, displays, and firmware can require different configurations. A
report for one model is not proof of compatibility with another.
Contributions should state the exact model and the hardware actually
tested.

## Privacy and Security

Before publishing files or opening an issue:

-   Remove `SystemSerialNumber`, `MLB`, `SystemUUID`, and other unique
    identifiers.
-   Review `config.plist`, logs, screenshots, and archives for personal
    information.
-   Do not upload private keys, account credentials, or unrelated
    personal files.
-   Share only the minimum configuration needed to reproduce an issue.
-   Preserve original backups privately.

## Contributing

Bug reports, verified fixes, hardware test results, and documentation
improvements are welcome.

### Issue reports

Include as much of the following as is relevant:

-   Exact laptop model and hardware revision.
-   BIOS version.
-   macOS version and build.
-   OpenCore version and relevant kext/driver versions.
-   Steps to reproduce the issue.
-   Expected and actual results.
-   Sanitized logs and configuration excerpts.
-   Whether the issue occurs on a clean or previously modified
    configuration.

### Pull requests

-   Explain the problem and the proposed change.
-   Describe the hardware and software versions tested.
-   Include test evidence where possible.
-   Keep changes focused and documented.
-   Do not commit personal identifiers or third-party files unless
    redistribution is permitted.

## Licensing

The license for the original documentation and configuration files in
this repository should be stated in the root `LICENSE` file. Do not
claim that third-party software is covered by this repository's license.

Before publishing a license, decide exactly which original files it
covers and review any redistribution requirements for included
components. Third-party projects, drivers, kexts, firmware, and tools
remain under their own licenses and terms. Linking to an external
project does not grant permission to redistribute it.

## Disclaimer

This is an independent community research project. It is not affiliated
with, endorsed by, or supported by Apple or ASUS.

-   macOS and related Apple marks are trademarks of Apple Inc.
-   ASUS and TUF are trademarks of their respective owners.
-   Compatibility is limited to the exact configurations and features
    documented as tested.
-   Changes may cause boot failures, instability, data loss, or hardware
    features to stop working.
-   You are responsible for backing up data and evaluating the risks
    before making changes.
-   No warranty or guarantee of functionality is provided.

## Acknowledgements

Thanks to the developers and communities maintaining OpenCore, relevant
documentation, and third-party projects referenced during research. See
each upstream project's own documentation and license for details.

------------------------------------------------------------------------

**Contributions, reproducible test results, and constructive feedback
are welcome.**
