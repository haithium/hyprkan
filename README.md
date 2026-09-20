

[![Ceasefire Now](https://badge.techforpalestine.org/default)](https://techforpalestine.org/learn-more)

# Hyprkan ⌨️

A Linux app-aware layer switcher that dynamically changes [Kanata](https://github.com/jtroo/kanata)'s layers based on the focused window.

## Table of Contents

- [Features](#features)
- [Supported Environments](#supported-environments)
- [Installation](#installation)
- [Usage](#usage)
- [Options](#options)
- [Similar Projects](#similar-projects)

## Features

- App-aware Kanata layer switching based on window class or title.
- Execute shell commands when specific applications gain focus.
- Send [virtual keys](https://jtroo.github.io/config.html#virtual-keys) to automate input behavior.
- Move mouse to specific position _(Kanata Linux support pending)_.

## Supported Environments

- X11
- Wayland
  - [Hyprland](https://wiki.hypr.land)
  - [Sway](https://swaywm.org)
  - [Niri](https://github.com/YaLTeR/niri)

## Installation

Download [hyprkan](src/hyprkan.py) script and make it executable: `chmod +x hyprkan.py`

### Dependencies:

- python >= 3.8
- [kanata](https://github.com/jtroo/kanata) >= 1.8.1
- [i3ipc](https://pypi.org/project/i3ipc/) (for Sway support)
- [python-xlib](https://pypi.org/project/python-xlib/) (for X11 support)

### Add hyprkan to your PATH (Optional)

To run hyprkan from anywhere, see: [docs/setup-path](docs/setup-path.md)

### Setting Up as a Service (Optional)

To run hyprkan automatically, see: [docs/service](docs/service.md)

## Usage

After downloading hyprkan:

1. Ensure that Kanata is running as a TCP server with the `-p` option (e.g., `-p 10000`) enabled and properly configured.
2. Set your app rules in the [configuration](docs/config.md) file.
3. Run hyprkan using the same port number: `hyprkan -p 10000`

## Options

| Option                                   | Description                                                                                                    |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `-c`, `--config PATH`                    | Path to the JSON configuration file (default: `$XDG_CONFIG_HOME/kanata/apps.json`)                             |
| `-p`, `--port PORT`                      | Kanata server port (e.g., `10000`) or full address (e.g., `127.0.0.1:10000`)                                   |
| `--change-layer LAYER`                   | Switch to the specified layer and exit                                                                         |
| `--fake-key KEY_NAME ACTION`             | Trigger a virtual key action and exit                                                                          |
| `--set-mouse X Y`                        | Set mouse position to the integer coordinates (`X`, `Y`) and exit <br> ⚠️ This option is not supported on Linux as of Kanata `v1.8.1`. |
| `-h`, `--help`                           | Print the help message and exit                                                                                |
| `--current-layer-info`                   | Print detailed info about the current active Kanata layer and exit                                             |
| `--current-layer-name`                   | Print the current active Kanata layer and exit                                                                 |
| `-w`, `--current-window-info [SECONDS]`  | Print current window info and exit (optionally wait SECONDS before checking)                                   |
| `-l`, `--layers`                         | Print kanata layers as JSON and exit                                                                           |
| `--log-level {DEBUG,INFO,WARNING,ERROR}` | Set logging level (default: `WARNING`)                                                                         |
| `-d`, `--debug`                          | Set logging level to `DEBUG`                                                                                   |
| `-q`, `--quiet`                          | Set logging level to `ERROR`                                                                                   |
| `-v`, `--version`                        | Show hyprkan version                                                                                           |

### ⚠️ Note on Performance

These options create a new TCP connection each time and are not suited for repeated use: `--change-layer`, `--layers`, `--current-layer-name`, `--current-layer-info`, `--set-mouse`, and `--fake-key`.

Use them only for debugging or one-off tasks. For performance, prefer event-based switching.

## Similar Projects

- Linux
  - [nata](https://github.com/mdSlash/nata)
  - [qanata](https://github.com/veyxov/qanata)
- macOS
  - [kanata-vk-agent](https://github.com/devsunb/kanata-vk-agent)
- Windows
  - [komokana](https://github.com/LGUG2Z/komokana)
  - [kanawin](https://github.com/Aqaao/kanawin)
