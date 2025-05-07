# Cursor Wayland Launcher

A simple launcher script for Cursor editor on Linux that automatically enables Wayland support.

## What is this?

This script serves as a wrapper for the Cursor editor AppImage, automatically adding Wayland-specific command line arguments to improve compatibility and performance on Linux systems running Wayland.

## Features

- Automatically finds the latest Cursor AppImage in your Downloads folder
- Adds Wayland support flags to every Cursor launch
- Preserves all command line arguments you pass to the editor
- Shows version information with `-v` or `--version`
- Displays help with `-h` or `--help`
- Includes debugging support with `--verbose`

## Installation

1. Download the script:
   ```bash
   wget -O cursor https://raw.githubusercontent.com/YOUR_USERNAME/cursor-wayland-launcher/main/cursor
   ```

2. Make it executable:
   ```bash
   chmod +x cursor
   ```

3. Move it to your system path:
   ```bash
   sudo mv cursor /usr/local/bin/
   ```

## Usage

Use the script just like you would use Cursor normally:

```bash
# Open Cursor in the current directory
cursor .

# Open a specific file
cursor /path/to/file.js

# Open a specific folder
cursor /path/to/project/
```

The script will automatically add the following flags:
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime
```

## Configuration

By default, the script looks for Cursor AppImage in your `~/Downloads/` directory. If you store your AppImage elsewhere, edit the `CURSOR_DIR` variable in the script.

## Requirements

- Bash shell
- `find` command
- A Wayland compositor (like GNOME on Wayland, KDE Plasma Wayland, Sway, etc.)
- Cursor AppImage downloaded to your Downloads folder (or the directory specified in `CURSOR_DIR`)

## Troubleshooting

If you encounter any issues:

1. Run the script with `--verbose` to see debug information
2. Make sure your Cursor AppImage has the correct filename format (`cursor-*x86_64.AppImage`)
3. Verify that the AppImage is in the expected directory
4. Ensure the AppImage has execute permissions

## License

MIT
