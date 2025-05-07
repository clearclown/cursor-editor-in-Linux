# Contributing to Cursor Wayland Launcher

Thank you for your interest in contributing to this project! This document provides guidelines for contributions and how to get started.

## Code of Conduct

Please be respectful and considerate in all interactions related to this project. We strive to maintain a welcoming and inclusive environment for everyone.

## Getting Started

1. **Fork the repository**
2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/cursor-wayland-launcher.git
   cd cursor-wayland-launcher
   ```
3. **Create a branch for your changes**
   ```bash
   git checkout -b feature/your-feature-name
   ```

## Making Changes

### For script improvements:

1. Make your changes to the `cursor` script
2. Test your changes thoroughly
3. Commit your changes with a descriptive message
4. Push to your fork and submit a pull request

### For documentation improvements:

1. Update the relevant Markdown files in the repository
2. Check your changes for spelling and grammar
3. Commit and push your changes
4. Submit a pull request

## Testing

Before submitting a pull request, please test your changes:

1. Install the modified script
2. Test all functionality:
   - Basic usage with paths
   - Version flag (`-v` or `--version`)
   - Help flag (`-h` or `--help`)
   - Verbose mode (`--verbose`)
   - Various path formats

## Pull Request Process

1. Update the README.md or other documentation with details of your changes if needed
2. Include a clear description of what your changes do and why they should be included
3. The pull request will be reviewed by maintainers who may suggest improvements or alternatives
4. Once approved, your changes will be merged

## Style Guidelines

### For bash script:

1. Use clear variable names
2. Add comments for complex operations
3. Follow standard bash conventions
4. Check for errors with `shellcheck` if possible

### For documentation:

1. Use clear and concise language
2. Follow Markdown best practices
3. Keep formatting consistent with existing documentation

## Reporting Issues

If you find a bug or have a suggestion:

1. Check if the issue already exists in the GitHub issues
2. Create a new issue if needed, including:
   - A clear title and description
   - Steps to reproduce if it's a bug
   - Your environment details (OS, Wayland compositor, etc.)
   - Any relevant logs or screenshots

## Feature Requests

Feature requests are welcome! Please include:

1. A clear description of the feature
2. Why it would be useful for the project
3. Any implementation ideas you have

Thank you for contributing!
