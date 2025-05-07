# Common Issues with Cursor on Linux

This document outlines common issues encountered when running Cursor on Linux systems and their solutions.

## Wayland Compatibility Issues

### Problem
Cursor, like many Electron-based applications, may have display or input issues when running on Wayland.

### Solution
This launcher automatically adds the following flags to enable proper Wayland support:
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime
```

## Path Handling Problems

### Problem
When launching Cursor with file or directory paths, it sometimes opens the home directory instead of the specified path.

### Solution
This launcher fixes path handling by ensuring command-line arguments are properly passed to the AppImage in the correct order.

## SUID Sandbox Errors

### Problem
You might see errors like:
```
[FATAL:setuid_sandbox_host.cc(158)] The SUID sandbox helper binary was found, but is not configured correctly.
Rather than run without sandboxing I'm aborting now.
You need to make sure that /tmp/.mount_cursor*/chrome-sandbox is owned by root and has mode 4755.
```

### Solution
This can be fixed by extracting the AppImage and setting the correct permissions:

```bash
# Extract the AppImage
./cursor-*x86_64.AppImage --appimage-extract

# Set correct permissions
sudo chown root:root squashfs-root/chrome-sandbox
sudo chmod 4755 squashfs-root/chrome-sandbox

# Run from extracted directory
./squashfs-root/AppRun
```

Alternatively, you can try running the AppImage with the `--no-sandbox` flag, but this is not recommended for security reasons.

## AppImage Not Found

### Problem
The launcher cannot find the Cursor AppImage.

### Solution
1. Make sure you have downloaded the Cursor AppImage
2. Verify it's in the directory specified by `CURSOR_DIR` in the script (default: `~/Downloads/`)
3. Check that the filename follows the expected pattern (`cursor-*x86_64.AppImage`)

## Launcher Not Working

### Problem
The launcher script itself doesn't work.

### Solution
1. Make sure the script has execute permissions: `chmod +x /usr/local/bin/cursor`
2. Verify that `/usr/local/bin` is in your PATH
3. Run the script with `--verbose` to see debug information

## Ubuntu 24.04 FUSE Issues

### Problem
Installing FUSE2 to run AppImages on Ubuntu 24.04 may break the system UI.

### Solution
1. Use the launcher script without installing FUSE
2. Extract the AppImage using `--appimage-extract` and run it from the extracted directory
3. Alternatively, use `--appimage-extract-and-run` when launching the AppImage

## GTK Module Errors

### Problem
You may see errors like:
```
Gtk-Message: Failed to load module "appmenu-gtk-module"
```

### Solution
These are usually harmless warnings and can be ignored. If they bother you, you can try installing the missing GTK modules:

```bash
sudo apt install appmenu-gtk-module
```

## Terminal Issues

### Problem
When running Cursor from the terminal, it doesn't properly detach or there are issues with terminal commands inside Cursor.

### Solution
Launch Cursor with `nohup` to properly detach it from the terminal:

```bash
nohup cursor &
```

## Desktop Integration

### Problem
Cursor doesn't show up in application menus or has no icon.

### Solution
Create a desktop entry file:

```bash
cat > ~/.local/share/applications/cursor.desktop << EOL
[Desktop Entry]
Name=Cursor AI
Comment=AI-powered code editor
Exec=/usr/local/bin/cursor %F
Icon=/opt/cursor.png
Type=Application
Categories=Development;IDE;
MimeType=text/plain;inode/directory;
StartupNotify=true
EOL
```

You'll need to download an icon for Cursor. You can use:
```bash
sudo wget -O /opt/cursor.png https://www.cursor.com/apple-touch-icon.png
```

## Logging In Issues

### Problem
Cannot log in to Cursor after installation.

### Solution
This is often related to browser cookie/session handling. Try:
1. Clearing browser cookies
2. Using a different browser for authentication
3. Ensuring your system time is correct
