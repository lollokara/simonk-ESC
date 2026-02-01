# macOS Build and Setup Instructions

This guide provides step-by-step instructions to set up your development environment on macOS for building and flashing the tgy firmware.

## Prerequisites

1.  **Terminal**: Open the Terminal app (found in Applications > Utilities).
2.  **Homebrew**: If you don't have Homebrew installed, install it by pasting the following command into your Terminal:

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

## Installation

### 1. Install Build Tools

You need `avra` (the assembler) and `avrdude` (for flashing). You also need `make`, which is usually included with macOS Xcode Command Line Tools.

Run the following commands in your Terminal:

```bash
# Install avra and avrdude
brew install avra avrdude

# Verify installations
avra --version
avrdude -v
make --version
```

If `make` is missing, install Xcode Command Line Tools:
```bash
xcode-select --install
```

### 2. Setup Visual Studio Code

VSCode is the preferred editor. We have configured it to support building and flashing directly.

1.  **Install VSCode**: Download and install from [code.visualstudio.com](https://code.visualstudio.com/).
2.  **Open the Project**: Open this repository folder in VSCode.
3.  **Install Recommended Extension**:
    -   When you open the folder, VSCode may ask to install "Recommended Extensions". Click **Install**.
    -   Alternatively, search for **`rockcat.avr-support`** in the Extensions view (Cmd+Shift+X) and install it. This provides syntax highlighting for AVR assembly.

## Building the Firmware

### Option A: Using VSCode Tasks (Recommended)

1.  Press **Cmd+Shift+P** to open the Command Palette.
2.  Type **Tasks: Run Build Task** (or press **Cmd+Shift+B** if configured as default).
3.  Select **Build All**.
    -   This will run `make all` and generate `.hex` files for all targets.

### Option B: Using the Terminal

1.  Open the integrated terminal in VSCode (**Ctrl+`**) or your external Terminal.
2.  Navigate to the project directory.
3.  Run:
    ```bash
    make all
    ```

## Flashing the Firmware

**Warning**: Ensure you have selected the correct target for your specific ESC hardware. Flashing the wrong target can damage your hardware.

### Option A: Using VSCode Tasks

1.  Press **Cmd+Shift+P** and select **Tasks: Run Task**.
2.  Select one of the Flash tasks depending on your programmer:
    -   **Flash (USBasp)**
    -   **Flash (AVRISP mkII)**
3.  You will be prompted to enter the **target name** (e.g., `tgy`, `bs_nfet`, `afro_nfet`). Enter the name corresponding to your board (without `.hex`).

### Option B: Using the Terminal

Run the make command for your programmer and target.

For USBasp:
```bash
make program_usbasp_tgy  # Replace 'tgy' with your specific target
```

For AVRISP mkII:
```bash
make program_avrisp2_tgy # Replace 'tgy' with your specific target
```

## Cleaning Up

To remove built files:
-   **VSCode**: Run the **Clean** task.
-   **Terminal**: Run `make clean`.
