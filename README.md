# ASUS-FA608PM-Hackintosh
OpenCore EFI and macOS compatibility research for ASUS TUF AMD laptops, starting with the FA608PM.
This project starts with the ASUS TUF Gaming FA608PM and aims to document its hardware compatibility, EFI configuration, known issues, and testing procedures. Future work may explore additional ASUS TUF laptops powered by AMD Zen 4 processors.

Project status: Experimental

简体中文

⸻

Table of Contents

* Project Overview
* Test Platform
* Hardware Compatibility
* Known Issues
* Project Structure
* Installation and Safety
* Contributing
* Disclaimer

Project Overview

The goals of this project are to:

* Maintain documented OpenCore EFI configurations.
* Record hardware compatibility across macOS versions.
* Document installation, testing, and troubleshooting procedures.
* Investigate compatibility with additional ASUS TUF AMD laptops.
* Encourage reproducible testing and community contributions.

This is an independent community project. It is not affiliated with Apple or ASUS.

Test Platform

The following information describes the initial test platform.

Component	Specification
Laptop	ASUS TUF Gaming FA608PM
CPU	AMD Ryzen 9 8940HX
Discrete GPU	NVIDIA GeForce RTX 5060 Laptop GPU, 8 GB
Operating System	macOS Tahoe 26.7.2
Wi-Fi	Realtek RTL8852CE
Bluetooth	Realtek USB Bluetooth, VID:PID 0489:E122

Hardware information and compatibility results apply only to the documented test system. Other configurations require separate verification.

Hardware Compatibility

Feature	Status	Notes
macOS boot	Verified	Boots on the documented test platform
Wi-Fi	Verified	Confirmed working on the test platform
Audio	Verified	Working configuration restored from a previously functional EFI
Bluetooth	Not Working	USB Bluetooth initialization remains unresolved
Display brightness	Not Working	Brightness control remains unresolved
NVIDIA graphics acceleration	Under Investigation	Actual driver functionality requires further verification
Sleep and wake	Untested	Requires dedicated testing
External displays	Untested	Requires dedicated testing
USB ports	Untested	Port-by-port verification is needed

Status definitions:

* Verified: Tested on the specified hardware.
* Partial: Some functionality works, but limitations remain.
* Experimental: Initial testing has been performed, but functionality is not fully validated.
* Untested: No adequate test results are available.
* Not Working: Tested and currently nonfunctional.
* Under Investigation: Testing is ongoing and the final status is not yet established.

A successful boot does not imply full hardware compatibility.

Known Issues

Bluetooth

The Realtek USB Bluetooth device has not been successfully initialized. Further investigation is required.

Display Brightness

Internal display brightness control is not yet working as expected.

NVIDIA Graphics

This project references the third-party NullMoth NVIDIA macOS Driver.

The presence of a supported driver project does not establish that the NVIDIA GPU is fully functional on this laptop. Driver loading, graphics acceleration, Metal support, and application behavior must be evaluated using actual test results.

Project Structure

The repository is intended to evolve toward the following structure:

ASUS-TUF-AMD-Hackintosh/
├── README.md
├── README_CN.md
├── LICENSE
├── THIRD-PARTY-LICENSES.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── docs/
│   ├── installation.md
│   ├── supported-models.md
│   ├── hardware-compatibility.md
│   ├── known-issues.md
│   └── troubleshooting.md
├── configs/
│   └── FA608PM/
│       ├── README.md
│       └── EFI/
└── tests/
    ├── test-plan.md
    └── results/

Files and directories will be added as the project develops.

Installation and Safety

Before using any EFI configuration:

1. Confirm that your laptop model matches the documented configuration.
2. Back up your existing EFI and important data.
3. Review the documented hardware limitations and known issues.
4. Check the versions and licenses of all included third-party components.
5. Test changes using a recoverable setup whenever possible.

Do not assume that an EFI configuration for one ASUS TUF laptop will work on another model, even if both use AMD Zen 4 processors.

Never publish personal device identifiers, including real serial numbers, MLB values, or SystemUUID values.

Contributing

Contributions are welcome, particularly:

* Reproducible hardware compatibility reports.
* Bug reports with sanitized logs.
* Verified fixes and configuration improvements.
* Installation and troubleshooting documentation.
* Compatibility research for additional ASUS TUF AMD laptops.

Please include the exact laptop model, BIOS version, macOS version, EFI version, and test results when reporting compatibility.

Remove personal information from logs and configuration files before submitting them.

Licensing

Third-party components remain subject to their respective licenses.

The repository’s licensing terms will be documented after reviewing the licensing conditions of its included components. Do not assume that every file in this repository is covered by a single license.

See THIRD-PARTY-LICENSES.md when available.

Disclaimer

This project is provided for research and educational purposes. Compatibility is limited to the hardware and software configurations explicitly documented as tested.

Modifying boot configurations or system settings may prevent a system from starting. Always maintain a recovery method and backups.

This project is not affiliated with, endorsed by, or supported by Apple or ASUS.
