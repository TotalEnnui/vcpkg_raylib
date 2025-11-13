<!-- omit in toc -->
# README.md

- [make VCPKG\_ROOT persistent](#make-vcpkg_root-persistent)
- [generate and then build ucrt64-release](#generate-and-then-build-ucrt64-release)
  - [from ucrt64 bash $](#from-ucrt64-bash-)
- [configure and build using ucrt64 gcc](#configure-and-build-using-ucrt64-gcc)
- [Add PowerShell to MSYS2 $PATH](#add-powershell-to-msys2-path)
- [Common Windows Libraries](#common-windows-libraries)
- [UCRT64 CMakePresets.json preset](#ucrt64-cmakepresetsjson-preset)
  - [using install](#using-install)
- [Add VCPKG to terminal path](#add-vcpkg-to-terminal-path)
  - [Get path to vcpkg.exe](#get-path-to-vcpkgexe)
- [install clarification](#install-clarification)
  - [ucrt64-gcc install](#ucrt64-gcc-install)
  - [MSVC install](#msvc-install)
- [🧬 Git Interactive Rebase: Clean History with Precision](#-git-interactive-rebase-clean-history-with-precision)
  - [🔧 Command Overview](#-command-overview)
  - [🛠️ Actions You Can Take](#️-actions-you-can-take)
- [Worktrees](#worktrees)
  - [Create a new worktree](#create-a-new-worktree)
    - [Steps to Create the Worktree](#steps-to-create-the-worktree)

## Create system link to allow MSYS UCRT64 to recognize c:\vcpkg <!-- omit in toc -->

from ucrt64 bash:

```bash- [make VCPKG\_ROOT persistent](#make-vcpkg_root-persistent)
- [generate and then build ucrt64-release](#generate-and-then-build-ucrt64-release)
  - [from ucrt64 bash $](#from-ucrt64-bash-)
- [configure and build using ucrt64 gcc](#configure-and-build-using-ucrt64-gcc)
- [Add PowerShell to MSYS2 $PATH](#add-powershell-to-msys2-path)
- [Common Windows Libraries](#common-windows-libraries)
- [UCRT64 CMakePresets.json preset](#ucrt64-cmakepresetsjson-preset)
  - [using install](#using-install)
- [Add VCPKG to terminal path](#add-vcpkg-to-terminal-path)
  - [Get path to vcpkg.exe](#get-path-to-vcpkgexe)
- [install clarification](#install-clarification)
  - [ucrt64-gcc install](#ucrt64-gcc-install)
  - [MSVC install](#msvc-install)
- [🧬 Git Interactive Rebase: Clean History with Precision](#-git-interactive-rebase-clean-history-with-precision)
  - [🔧 Command Overview](#-command-overview)
  - [🛠️ Actions You Can Take](#️-actions-you-can-take)

mkdir -p /usr/local/bin
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg
export VCPKG_ROOT=/c/vcpkg  
```

---

## make VCPKG_ROOT persistent

```Cmakepresets
echo 'export VCPKG_ROOT=/c/vcpkg' >> ~/.bashrc</br>
```

---

## generate and then build ucrt64-release

### from ucrt64 bash $

```bash
mkdir -p /usr/local/bin
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg
export VCPKG_ROOT=/c/vcpkg  
```

---

## configure and build using ucrt64 gcc

```bash
rm -rf build/ucrt64-gcc
cmake --preset ucrt64-gcc
cmake --build --preset ucrt64-gcc
```

---

## Add PowerShell to MSYS2 $PATH  

Bash:

```bash
export PATH="/c/Windows/System32/WindowsPowerShell/v1.0:$PATH"
```

---

## Common Windows Libraries

| Library      | Purpose                                         |
|--------------|------------------------------------------------|
| `kernel32`   | Core Windows API: memory, processes, threads, file I/O |
| `user32`     | GUI: windows, messages, input, dialogs         |
| `gdi32`      | Graphics: drawing, fonts, bitmaps              |
| `winmm`      | Multimedia: timers, sound, joystick            |
| `shell32`    | Shell operations: file dialogs, launching apps |
| `ole32`      | COM object support                             |
| `oleaut32`   | Automation support for COM                     |
| `uuid`       | GUID generation and COM identifiers            |

Windows libraries location: C:\Program Files (x86)\Windows Kits\10\Lib\10.0.26100.0\um\x64

---

## UCRT64 CMakePresets.json preset

It was necessary because `VCPKG_APPLOCAL_DEPS` controls whether vcpkg runs a post-build PowerShell script (`applocal.ps1`) to copy runtime dependencies next to your binary. MSYS2 does not recognize PowerShell.

`"VCPKG_APPLOCAL_DEPS": "OFF"`

### using install

`cmake --install ./build/ucrt64-gcc`

---

## Add VCPKG to terminal path

`$env:PATH += ";C:\vcpkg"`

### Get path to vcpkg.exe

`Get-Command vcpkg`

---

## install clarification

vs code taskbar configuration only does configurations and build, NOT install. Install must be initiated via terminal, bash (gcc), or developer PowerShell (MSVC). Outputs just outputs but install installs, in order to maintain separation.

### ucrt64-gcc install

```bash
cmake --install build/ucrt64-gcc
```

### MSVC install

> Why the Command Line Works Better for `cmake --install`

- VS Code’s Quick Bar (e.g. “CMake: Install”) doesn’t always pass the `--config` Release flag.
- Without that flag, CMake doesn’t know which subdirectory (Release/, Debug/, etc.) to glob DLLs from — so your install(CODE ...) block silently finds nothing.
- The command line gives you full control, especially for reproducible install-time logic like your DLL copy step.

> Best practices in Powershell or the VS Code terminal:

```Powershell
cmake --preset MSVC-manifest
cmake --build --preset MSVC-manifest --config Release
cmake --install build/MSVC-manifest --config Release
```

---

## 🧬 Git Interactive Rebase: Clean History with Precision

Interactive rebase lets you rewrite commit history to polish your work before sharing or merging. It’s ideal for teaching commit hygiene, modular rollback, and reproducible workflows.

---

### 🔧 Command Overview

```bash
git rebase -i HEAD~N
```

- HEAD~N: Rebase the last N commits
- -i: Launches an interactive editor
- `esc :q` to exit without changes

### 🛠️ Actions You Can Take

| Command | Description                                   |
|---------|-----------------------------------------------|
| pick    | Keep commit as-is                             |
| reword  | Edit commit message                           |
| edit    | Pause to modify commit contents               |
| squash  | Merge with previous commit (combine messages) |
| fixup   | Merge with previous commit (discard message)  |
| drop    | Delete the commit                             |

## Worktrees

### Create a new worktree

#### Steps to Create the Worktree

1. Navigate to your repo root:

    ```bash
    cd ~/Documents/repos/vcpkg_raylib
    ```4.

2. Create the worktree:

    ```bash
    git worktree add ../vcpkg_raylib_new_feature -b new_feature
    ```

    > This creates a new branch called `new_feature` and checks it out in a sibling directory `../vcpkg_raylib_new_feature`.

3. Verify it’s active:

    ```bash
    git worktree list
    ```

    > You should see both the main repo and the new worktree listed.

4. Open the new worktree in VS Code:

    - Use **File → Open Folder** and select `../vcpkg_raylib_new_feature`.
    - Or run:

    ```bash
    code ../vcpkg_raylib_new_feature
    ```
