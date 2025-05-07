# Installation Guide

This document provides detailed instructions for installing and setting up the Cursor Wayland Launcher script.

## Prerequisites

- Linux distribution with Wayland support
- Bash shell
- `find` command
- Cursor editor AppImage

## Basic Installation

1. **Download the script**

   ```bash
   wget -O cursor https://raw.githubusercontent.com/YOUR_USERNAME/cursor-wayland-launcher/main/cursor
   ```

2. **Make it executable**

   ```bash
   chmod +x cursor
   ```

3. **Install system-wide**

   ```bash
   sudo mv cursor /usr/local/bin/
   ```

4. **Verify installation**

   ```bash
   cursor --version
   ```

## Alternative Installation Methods   ```

### Manual Installation

1. **Clone this repository**

   ```bash
   git clone git@github.com:clearclown/cursor-editor-in-Linux.git
   ```

2. **Copy the script**

   ```bash
   cd cursor-wayland-launcher
   chmod +x cursor
   sudo cp cursor /usr/local/bin/
   ```

## Customizing the Installation

### Using a different AppImage location

If you store your Cursor AppImage in a location other than `~/Downloads/`, you'll need to edit the script:

1. Open the script in a text editor:

   ```bash
   sudo nano /usr/local/bin/cursor
   ```

2. Find this line near the beginning:

   ```bash
   CURSOR_DIR="$HOME/Downloads/"
   ```

3. Change it to your preferred location, for example:

   ```bash
   CURSOR_DIR="$HOME/Applications/"
   ```

4. Save and close the editor.

### Creating a desktop entry

To create a desktop entry for Cursor with Wayland support:

1. Create a new `.desktop` file:

   ```bash
   nano ~/.local/share/applications/cursor-wayland.desktop
   ```

2. Add the following content:

   ```
   [Desktop Entry]
   Name=Cursor (Wayland)
   Comment=Cursor Editor with Wayland Support
   Exec=cursor %F
   Icon=cursor
   Type=Application
   Categories=Development;IDE;
   MimeType=text/plain;inode/directory;
   StartupNotify=true
   StartupWMClass=Cursor
   ```

3. Make it executable:

   ```bash
   chmod +x ~/.local/share/applications/cursor-wayland.desktop
   ```

## Troubleshooting

### Script cannot find Cursor AppImage

If you see an error like:

```
Error: Cursor AppImage not found in /home/user/Downloads/
Please ensure Cursor AppImage is installed in /home/user/Downloads/
```

Make sure:
1. You have downloaded the Cursor AppImage
2. It has the correct naming format (`cursor-*x86_64.AppImage`)
3. It's in the directory specified by the `CURSOR_DIR` variable in the script

### Permission denied

If you get a "Permission denied" error, make sure the script is executable:

```bash
sudo chmod +x /usr/local/bin/cursor
```

### Command not found

If `cursor` command is not found, ensure:
1. The script is in a directory that's in your PATH
2. You've reloaded your shell configuration if you modified PATH
