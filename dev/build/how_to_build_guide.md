# R-Type: Reborn - Build and Release Documentation

Welcome to the documentation for building and releasing **R-Type: Reborn**! This guide will help you compile the project from source, create releases, and understand the differences between building and releasing. Let's dive in!

## Build vs. Release

- **Build**: The process of compiling source code into an executable format. Building is typically used during development to test new features, debug, and make changes. A build may have debug symbols and other information useful for developers.
- **Release**: A finalized version of the software intended for end-users. A release includes all dependencies and is optimized for performance, ensuring users can run the software without requiring the development environment.

## Dependencies & Requirements

To build and run the project, you will need:

- **C++** compiler supporting C++17 or later
- **SFML** (Simple and Fast Multimedia Library) for graphics, audio, and input handling
- **CMake** for building the project
- **GLM** (OpenGL Mathematics) for vector and matrix operations
- **Conan** for managing dependencies

Install the dependencies using the package manager for your platform, or refer to the official documentation for each tool.

## Supported Platforms

- Windows 10+
- Linux (Fedora, Ubuntu, etc.)

## Build Instructions

To build **R-Type: Reborn**, follow these steps:

*Note: These instructions are used to recompile the project from source. If you just want to run the game without compiling it, see the [Quick Start](#quick-start) section.*

### Windows

1. Clone the repository to your local machine.
2. Open a terminal and navigate to the project directory.
3. Launch the following command:
   ```bash
   ./build-windows.ps1
   ```
4. Accept the installation of the dependencies.
5. You can run the project by launching the executable in the `build` directory or by running the `r-type_client` and `r-type_server` executables at the root of the project.

### Linux

1. Clone the repository to your local machine.
2. Open a terminal and navigate to the project directory.
3. Launch the following command (you need to have sudo rights):
   ```bash
   sudo ./build-linux.sh
   ```
4. Accept the installation of the dependencies.
5. You can run the project by launching the executable in the `build` directory or by running the `r-type_client` and `r-type_server` executables at the root of the project.

## Release Instructions

To create a release of **R-Type: Reborn**, follow these steps:

### Windows

1. Clone the repository to your local machine.
2. Follow the build instructions [here](#build-instructions).
3. Launch the following command:
   ```bash
   ./release-windows.ps1
   ```
4. The release will be in the `build` directory.
5. You can run the project by launching the executable in the `build` directory or by running the `R-type-Reborn-version-win64.exe` executable at the root of the project.

### Linux

1. Clone the repository to your local machine.
2. Follow the build instructions [here](#build-instructions).
3. Launch the following command:
   ```bash
   sudo ./release-linux.sh
   ```
4. The release will be in the `build` directory.
5. You can run the project by launching the executable in the `build` directory or by running the `R-type-Reborn-version-Linux.rpm` executable at the root of the project.

