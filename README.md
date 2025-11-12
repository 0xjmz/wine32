# Wine32 Container Script

## Overview

The Wine32 Container Script provides a clean and isolated environment for running Wine in pure 32-bit mode inside a container.
Unlike WoW64-based setups, this approach uses genuine 32-bit libraries and dependencies, ensuring better compatibility and performance for legacy Windows applications.

This script is particularly useful on modern 64-bit systems where native 32-bit support may be limited or deprecated.

---

## Prerequisites

Before using the script, ensure that Podman is installed and configured correctly on your system.

### 1. Install Podman

On Arch Linux or derivatives:

```bash
sudo pacman -Syu
sudo pacman -S podman
```

### 2. Configure user namespaces

Podman requires proper user namespace mappings.\
Edit the following configuration files as root:

#### `/etc/subuid`

```bash
sudo nano /etc/subuid
```

Add (replace `yourusername` with your actual username):

```
yourusername:100000:65536
```

#### `/etc/subgid`

```bash
sudo nano /etc/subgid
```

Add the same line:

```
yourusername:100000:65536
```

---

## Installation

To install the script system-wide, copy it to a directory that is part of your `$PATH`, such as `/usr/local/bin` or `/usr/bin`.

Example:

```bash
sudo cp -i wine32 /usr/local/bin
```

You can then verify that it is accessible:

```bash
which wine32
```

---

## Usage

### Basic usage

To run Wine in 32-bit mode:

```bash
wine32
```

The script will automatically:

- Build a Podman container (if not already present),
- Download the appropriate 32-bit Wine packages from [dl.winehq.org](https://dl.winehq.org/),
- Launch Wine within a 32-bit containerized environment.

### Specify a Wine version

To run a specific Wine version:

```bash
WINEVER=10.10 wine32
```

### Use a custom Wine prefix

To specify an alternative Wine prefix directory:

```bash
WINEPREFIX=~/.wine-32 wine32
```

By default, the prefix is located at:

```
~/.wine-32
```

---

## Compatibility

This script can coexist with the Wine package provided by the Arch Linux official repositories.\
Running `wine32` does not interfere with your system-wide Wine configuration or prefixes.

