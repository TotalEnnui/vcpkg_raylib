# Create system link to allow MSYS UCRT64 to recognize c:\vcpkg

from ucrt64 bash:

```bash
mkdir -p /usr/local/bin
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg
export VCPKG_ROOT=/c/vcpkg  
```

## make VCPKG_ROOT persistent

```Cmakepresets
echo 'export VCPKG_ROOT=/c/vcpkg' >> ~/.bashrc</br>
```

## generate and then build ucrt64-release

### from ucrt64 bash $

```bash
mkdir -p /usr/local/bin
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg
export VCPKG_ROOT=/c/vcpkg  
```

## configure and build using ucrt64 gcc

```bash
rm -rf build/ucrt64-gcc
cmake --preset ucrt64-gcc
cmake --build --preset ucrt64-gcc
```

## Add PowerShell to MSYS2 $PATH  

Bash:

```bash
export PATH="/c/Windows/System32/WindowsPowerShell/v1.0:$PATH"
```

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

## UCRT64 CMakePresets.json preset

It was necessary because `VCPKG_APPLOCAL_DEPS` controls whether vcpkg runs a post-build PowerShell script (`applocal.ps1`) to copy runtime dependencies next to your binary. MSYS2 does not recognize PowerShell.

`"VCPKG_APPLOCAL_DEPS": "OFF"`

### using install

`cmake --install ./build/ucrt64-gcc`

## Add VCPKG to terminal path

`$env:PATH += ";C:\vcpkg"`

### Get path to vcpkg.exe

`Get-Command vcpkg`

## install clarification

vs code taskbar configuration only does configurations and build, NOT install. Install must be initiated via terminal, bash (gcc), or developer PowerShell (MSVC). Outputs just outputs but install installs, in order to maintain separation.

### ucrt64-gcc install

```bash
cmake --install build/ucrt64-gcc
```

### MSVC install

```Powershell
cmake --install build/release --config Release
```
