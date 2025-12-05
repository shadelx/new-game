# New Game

A C++ project built with CMake, vcpkg, and MinGW.

## Prerequisites

- **MinGW**: C++ compiler for Windows
- **CMake**: Version 3.10 or later
- **vcpkg**: Package manager for C++ libraries
- **VCPKG_ROOT**: Environment variable pointing to your vcpkg installation

## Project Structure

```
new-game/
├── CMakeLists.txt           # CMake build configuration
├── CMakePresets.json        # CMake presets with vcpkg integration
├── vcpkg.json               # vcpkg manifest with dependencies
├── src/
│   └── main.cpp             # Main application source
├── build/                   # Build output directory (generated)
└── README.md                # This file
```

## Dependencies

- **fmt** (12.1.0): A modern C++ formatting library
- **curl** (8.17.0): Library for transferring data with URLs
- **zlib** (1.3.1): Compression library (transitive dependency of curl)

## Building

### Step 1: Configure the project

```bash
cmake --preset vcpkg
```

This command:

- Uses the `vcpkg` preset from `CMakePresets.json`
- Automatically runs `vcpkg install` to fetch dependencies
- Configures the build using MinGW Makefiles

### Step 2: Build the project

```bash
cmake --build build
```

Or use make directly:

```bash
cd build
make
```

## Running

After building, run the executable:

```bash
./build/new-game.exe
```

## Configuration

### CMake Presets

The project uses CMake presets defined in `CMakePresets.json`:

- **vcpkg**: Uses x64-mingw-static triplet for static linking
- **default**: Inherits from vcpkg preset with custom environment variables

### vcpkg Configuration

Dependencies are specified in `vcpkg.json` using manifest mode. The project uses:

- **VCPKG_TARGET_TRIPLET**: `x64-mingw-static` (target platform)
- **VCPKG_HOST_TRIPLET**: `x64-mingw-static` (host tools platform)

### Static vs Dynamic Linking

This project uses **static linking** (`x64-mingw-static`) which means:

- ✅ Executable works standalone without DLL files
- ✅ Simpler distribution
- ❌ Larger executable size

To switch to dynamic linking, change `x64-mingw-static` to `x64-mingw-dynamic` in `CMakePresets.json`.

## Development

### Adding New Dependencies

1. Edit `vcpkg.json` and add the package name to the `dependencies` array
2. Run `cmake --preset vcpkg` to install and configure

Example:

```json
{
  "dependencies": ["fmt", "curl", "sqlite3"]
}
```

### Building in Debug Mode

```bash
cmake --preset vcpkg -DCMAKE_BUILD_TYPE=Debug
cmake --build build --config Debug
```

### Cleaning the Build

```bash
rm -rf build
```

## Troubleshooting

### CMake errors about missing fmt/curl

Make sure to use the `vcpkg` preset:

```bash
cmake --preset vcpkg
```

### Missing DLL errors when running

If using dynamic linking (`x64-mingw-dynamic`), ensure DLL files are in the PATH or build directory.

### vcpkg errors about Visual Studio

The project is configured for MinGW, not Visual Studio. Ensure:

- `VCPKG_ROOT` environment variable is set
- MinGW is installed and in your PATH

## Links

- [vcpkg Documentation](https://github.com/microsoft/vcpkg)
- [fmt Library](https://github.com/fmtlib/fmt)
- [curl Library](https://curl.se/)
- [CMake Documentation](https://cmake.org/)
