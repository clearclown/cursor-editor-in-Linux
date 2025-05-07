# Cursor Editor Linux Launcher

A robust launcher script for Cursor AI editor on Linux that enhances compatibility with Wayland and provides additional features for Linux users.

## What is Cursor?

Cursor is an AI-powered code editor designed for pair programming with AI. It's a fork of Visual Studio Code with additional AI features like code generation, smart rewrites, and codebase queries. It allows developers to write code using natural language instructions and integrates advanced AI capabilities for enhanced productivity.

## Features of This Launcher

- **Wayland Optimization**: Automatically adds Wayland-specific flags for better compatibility
- **AppImage Management**: Automatically finds and uses the latest Cursor AppImage
- **Command Line Support**: Preserves all command line arguments you pass to the editor
- **Metadata Access**: Shows version information with `-v` or `--version`
- **Help System**: Displays help with `-h` or `--help`
- **Debugging Tools**: Includes debugging support with `--verbose`
- **Permissions Handling**: Automatically checks and sets executable permissions
- **Path Handling**: Correctly handles file and directory paths

## Installation

1. Download the script:
   ```bash
   wget -O cursor https://raw.githubusercontent.com/clearclown/cursor-editor-in-Linux/main/cursor
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

# Get version information
cursor -v

# Get help
cursor -h

# Run with debug info
cursor --verbose
```

The script will automatically add the following flags for Wayland support:
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime
```

## Why Use This Launcher?

Cursor is available as an AppImage on Linux, which doesn't require traditional installation but can be tricky to set up properly. This launcher script addresses several common issues with running Cursor on Linux:

1. **Wayland Support**: Improves compatibility with Wayland display server
2. **Path Resolution**: Fixes issues with file and directory path handling
3. **AppImage Management**: Eliminates the need to manually locate and execute the AppImage
4. **Permissions**: Automatically handles executable permissions
5. **Integration**: Provides proper system integration with version information and help

## Configuration

By default, the script looks for Cursor AppImage in your `~/Downloads/` directory. If you store your AppImage elsewhere, edit the `CURSOR_DIR` variable in the script.

## About Cursor's Features

Cursor offers several AI-powered features including:
- Autocomplete and code prediction that adapts based on recent changes
- Code generation that understands context
- Multi-line edit suggestions

As it's a fork of Visual Studio Code, existing extensions and settings can be integrated into your workflow.

## Requirements

- Bash shell
- `find` command
- Cursor AppImage downloaded to your Downloads folder (or the directory specified in `CURSOR_DIR`)
- For Wayland support: A Wayland compositor (like GNOME on Wayland, KDE Plasma Wayland, Sway, etc.)

## Troubleshooting

If you encounter any issues:

1. Run the script with `--verbose` to see debug information
2. Make sure your Cursor AppImage has the correct filename format (`cursor-*x86_64.AppImage`)
3. Verify that the AppImage is in the expected directory
4. Ensure the AppImage has execute permissions
5. If you see SUID sandbox errors, you may need to adjust permissions on the chrome-sandbox file

## License

MIT
