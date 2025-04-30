# comm-package-rebuild for Arch Linux

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.1.1-blue.svg" alt="Version"/>
  <img src="https://img.shields.io/badge/Arch-Linux-1793D1.svg?logo=arch-linux" alt="Arch Linux"/>
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License"/>
</p>

## Overview

comm-package-rebuild is a powerful bash utility designed to rebuild installable packages from already installed software on Arch Linux and Arch-based distributions. The tool extracts installed files, generates proper metadata, and packages everything into a format compatible with the pacman package manager.

This tool is particularly valuable for:
- System administrators who need to replicate custom packages across multiple systems
- Package maintainers working on modifications to existing packages
- Advanced users who want to backup or distribute modified packages
- Troubleshooting and analyzing package contents

## Features

- **Complete Package Rebuilding**: Rebuilds packages from installed files with proper structure
- **Modern Interface**: Features an elegant, color-coded terminal interface for better readability
- **Comprehensive Metadata**: Generates proper .PKGINFO and .MTREE files with dependencies
- **Compression Support**: Creates optimized zstd-compressed packages compatible with pacman
- **Verification**: Automatically generates MD5 checksums for package integrity
- **Permissions Handling**: Properly manages file permissions and ownership
- **Detailed Reporting**: Provides size information and progress updates
- **Cleanup Options**: Offers optional cleanup of temporary files

## Requirements

- Arch Linux or an Arch-based distribution (Manjaro, BigLinux, EndeavourOS, etc.)
- `pacman` package manager
- `fakeroot` for proper permission handling
- `sudo` for accessing system files
- `bsdtar` for archive creation
- `zstd` compression support

## Installation

### Option 1: Install from Arch Repository

```bash
# Install the package from Arch repository
sudo pacman -S comm-package-rebuild
```

### Option 2: Manual Installation

```bash
# Clone the repository
git clone https://github.com/talesam/comm-package-rebuild.git

# Navigate to the directory
cd comm-package-rebuild

# Install using makepkg
makepkg -si
```

## Usage

### Basic Usage

Run the executable with the name of the installed package you want to rebuild:

```bash
pkg-rebuild package_name
```

### Examples

**Rebuild Firefox package:**
```bash
pkg-rebuild firefox
```

**Rebuild multiple packages:**
```bash
for pkg in firefox libreoffice-fresh vlc; do
  pkg-rebuild $pkg
done
```

**Rebuild a package with a custom output directory:**
```bash
OUTPUT_DIR=/custom/path pkg-rebuild package_name
```

## Visual Interface

The script features a modern, color-coded interface that:
- Uses blue, cyan, and white for standard operations
- Highlights success messages in green
- Shows warnings in yellow
- Displays errors in red
- Provides clear step-by-step progress indicators

## Output Files

The script creates the following files:

- **Rebuilt Package**: `~/rebuilt_packages/package_name-version-arch.pkg.tar.zst`
- **MD5 Checksum**: `~/rebuilt_packages/package_name-version-arch.pkg.tar.zst.md5`
- **Temporary Files** (if not cleaned): `~/package_rebuild_package_name/`

## Advanced Usage

### Installing Rebuilt Packages

After creating a package, you can install it using:

```bash
sudo pacman -U ~/rebuilt_packages/package_name-version-arch.pkg.tar.zst
```

### Distributing Packages

Rebuilt packages can be distributed to other Arch-based systems. However, be aware of:
- Architecture compatibility
- Dependency requirements
- License restrictions

### Customization

You can modify the script to change:
- Output directory: Edit the `outputDir` variable
- Compression method: Modify the `bsdtar` command options
- Color scheme: Adjust the color definition variables

## Troubleshooting

### Common Issues

**Permission denied errors:**
- Make sure you're running the script with sudo privileges for reading system files

**Package not found:**
- Verify the package is installed using `pacman -Q package_name`

**Missing dependencies in rebuilt package:**
- Dependencies are copied from the installed package; ensure all dependencies were correctly installed

**Disk space issues:**
- Check available space in your home directory for temporary files
- Large packages may require significant temporary space

## Contributing

Contributions are welcome! Here's how you can contribute:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Original concept and implementation by Tales A. Mendonça (talesam@gmail.com)
- Color scheme and interface improvements by the Community team
- Thanks to the Arch Linux community for their extensive documentation and tools

## Disclaimer

This script is not officially associated with or endorsed by Arch Linux or any of its derivatives. Use it responsibly and at your own risk. The rebuilt packages may not be identical to the original packages, especially if system configurations have been modified.
