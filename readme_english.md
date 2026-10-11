# GCC Developer Air (GDA) - Beta Release

A lightweight, highly extensible Integrated Development Environment (IDE) built on Python and PySide6. Designed as a "developer's toolbox," it seamlessly integrates a unified virtual file system that eliminates the boundaries between local and remote environments, alongside versatile terminals and Language Server Protocol (LSP) support.

## 📦 About This Beta Release (Core IDE Only)
This release serves as an **early access preview of the core IDE system**.

*   **No Embedded Toolchains Included:** This version does not include compilers, flashers, or embedded-specific toolchains. It is provided as a "blank slate" base system.
*   **What is Included:** The core editor, a standalone Python runtime environment, LSPs (`clangd` / `pylsp`), built-in terminals, the Virtual File System (VFS), and AI chat integration.
*   **Bundled Python Environment:** Includes the base Python interpreter required to run the IDE itself, along with essential libraries that allow for basic script execution and testing out of the box.

## 🧰 Custom-Built & Bundled Dependencies
To prioritize a "ready-to-use" experience and avoid polluting the host PC's Python or C++ build environments, GDA bundles critical components that typically require manual compilation or complex setup. These have been **custom-built and packaged as standalone components**.

*   **Standalone LSP Servers**
    *   **`pylsp.exe`**: Built from source into a single executable using PyInstaller to sever dependencies on the host Python environment.
    *   **`clangd.exe`**: The powerful C/C++ Language Server, extracted directly from the MSYS2 (UCRT64) environment and bundled standalone.
*   **MSYS2 (Minimal GDA Subset)**
    *   Includes a portable, minimal subset of `msys64/usr` tools (such as `make` and `bash`) required for building and operating the integrated terminals. Users do not need to install MSYS2 on their host machines.
*   **PySide6-QtAds (Fully Exported Custom Build)**
    *   The Python binding for the Advanced Docking System, which forms the backbone of our docking UI.
    *   This is a **heavily modified build patched via CMake and C++ headers to export all internal symbols**, allowing direct Python control over internal classes (like `CDockOverlayCross`) that are inaccessible in the standard release. It includes hidden loading mechanisms to prevent conflicts with native system libraries.
*   **Communication & Formatting Utilities**
    *   **`muxserial`**: Our proprietary, transparent serial port multiplexer.
    *   **`yapf_third_party`**: A Python formatter. Included as a substitute fork due to the current maintenance status of the original `yapf`.
*   **Dedicated Developer Font**
    *   **`PlemolJPConsoleNF`**: Bundled as the standard font to prevent text corruption (including Nerd Fonts icons) in the editor and terminals, strictly enforcing monospaced rendering for optimal visibility.

## 🛠 Key Features & Keywords

A practical feature set designed to resolve real-world development hurdles.

**Text Editor & LSP (Language Server Protocol)**
*   **Multi-Text Editor:** Docking UI for flexible split-pane layouts and simultaneous multi-file editing.
*   **C/C++ & Python Support:** Fully integrates `clangd` and `pylsp` for real-time autocomplete, Go to Definition/References (tag jumping), and static code analysis (error highlighting).
*   **Omnibox:** Combines incremental search, bulk replace, editor commands, instant Python script execution, and AI assistance into a single input interface.

**Virtual File System (VFS) & Filer**
*   **Transparent File Operations:** Mount and manipulate local PC, SFTP (SSH), and MicroPython file systems within the same unified tree UI.
*   **Auto-Sync:** Automatic detection of local file changes and differential sync functionality for remote environments.
*   **Drag & Drop:** Seamless file transfer across different protocols (e.g., from Local to SFTP).

**Integrated Terminals & Remote Connections**
*   **Dedicated Terminals:** Manage Bash, SSH, Serial Monitor, and Python/MicroPython REPL sessions via a tabbed interface.
*   **ANSI Escape Code Support:** Terminal rendering with basic escape sequence support.
*   **Multi-Protocol Management:** Centralized management of essential development communication protocols, including SSH, Telnet, SFTP, and Serial connections.

**AI Assistance & Automation**
*   **Integrated AI Chat:** Interactive assistant supporting major LLM backends, docked directly within the UI.
*   **Foundation for External Tools:** Built-in frameworks for GUI-based Makefile generation and DAP (Debug Adapter Protocol) inspectors, laying the groundwork for future embedded toolchain integration.