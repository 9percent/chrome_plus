# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Chrome++ is a Windows DLL enhancement for Chrome/Chromium-based browsers that provides tab management improvements, mouse gestures, and portable mode functionality. The project is built as a DLL (`version.dll`) that gets injected into Chrome to enhance its functionality.

## Build System

The project uses Xmake as the build system:

### Building
```bash
# Configure for specific architecture
xmake f -a x64 --toolchain=clang-cl --yes

# Build the project
xmake

# Available architectures: x86, x64, arm64
```

### Build Configuration
- **Debug**: Uses MTd runtime, includes debug symbols
- **Release**: Uses MT runtime, enables optimizations, includes vc-ltl5 for reduced size
- **Output**: `version.dll` placed in `build/release/` (release mode)

### Dependencies
- **Detours**: Microsoft's library for hooking Windows API calls (included as submodule)
- **vc-ltl5**: Visual C++ Lightweight Runtime (release builds only)
- Windows libraries: onecore, propsys, oleacc

## Architecture

### Core Components

- **Main Entry** (`src/chrome++.cc`): Main DLL initialization and coordination
- **Configuration** (`src/config.cc/.h`): INI file parsing and settings management
- **Hooking** (`src/hijack.cc/.h`): System DLL loading and API hooking setup
- **Tab Management** (`src/tabbookmark.cc/.h`): Tab behavior enhancements
- **Portable Mode** (`src/portable.cc/.h`): Portable Chrome functionality
- **Hotkeys** (`src/hotkey.cc/.h`): Keyboard shortcut handling
- **PAK Patching** (`src/pakpatch.cc/.h`): Chrome resource file modification
- **Utils** (`src/utils.cc/.h`): Common utility functions

### Configuration System
- **File**: `src/chrome++.ini` (copied to output directory)
- **Format**: Windows INI with sections for `[general]` and `[tabs]`
- **Environment Variables**: Supports `%app%` (Chrome exe directory) and standard Windows variables
- **Key Settings**: Tab behavior, mouse gestures, portable paths, custom command-line switches

### Key Features
1. **Tab Enhancements**: Double-click close, right-click close, wheel scrolling, keep last tab
2. **Mouse Gestures**: Tab switching with wheel, new tab creation for URLs/bookmarks
3. **Portable Mode**: Custom data/cache directories, profile isolation
4. **Hotkeys**: Boss key (hide/restore), translation shortcut
5. **Chrome Integration**: App ID setting, command-line argument handling

### Hooking Strategy
Uses Microsoft Detours to intercept Windows API calls:
- Chrome startup processes
- File system operations (for portable mode)
- Window messages (for mouse/keyboard handling)
- UI element interactions

## Development Workflow

### Testing Changes
1. Build the DLL: `xmake`
2. Copy `version.dll` to Chrome directory alongside `chrome.exe`
3. Copy `chrome++.ini` to same directory for configuration
4. Launch Chrome to test functionality

### Version Management
- Version defined in `src/version.h` (RELEASE_VER_MAIN/SUB/FIX)
- CI/CD automatically updates version for releases
- Alpha builds use commit hash for version string

### Multi-Architecture Support
- Supports x86, x64, and ARM64 architectures
- GitHub Actions builds all architectures in parallel
- Conditional compilation for architecture-specific Detours code

## Important Notes

- This is a Windows-only project that requires Microsoft toolchain
- The DLL hooks into Chrome processes - requires careful testing
- Configuration changes may require browser restart
- Chrome compatibility varies by version - tested mainly on latest stable
- Uses C++20 features and Windows Unicode APIs throughout