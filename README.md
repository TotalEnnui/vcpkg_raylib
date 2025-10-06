## Create system link to allow MSYS UCRT64 to recognize c:\vcpkg 
from ucrt64 bash:

```
mkdir -p /usr/local/bin
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg
export VCPKG_ROOT=/c/vcpkg  
```

## make VCPKG_ROOT persistent
```
echo 'export VCPKG_ROOT=/c/vcpkg' >> ~/.bashrc</br>
```

## generate and then build ucrt64-release
from ucrt64 bash $

```  
rm -rf build/ucrt64-gcc
cmake --preset ucrt64-gcc
cmake --build --preset ucrt64-gcc
```

## Add PowerShell to MSYS2 $PATH  
Bash:
```
export PATH="/c/Windows/System32/WindowsPowerShell/v1.0:$PATH"
```
## Common Windows Libraries
<table>
  <thead>k
    <tr>
      <th>Library</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>kernel32</code></td>
      <td>Core Windows API: memory, processes, threads, file I/O</td>
    </tr>
    <tr>
      <td><code>user32</code></td>
      <td>GUI: windows, messages, input, dialogs</td>
    </tr>
    <tr>
      <td><code>gdi32</code></td>
      <td>Graphics: drawing, fonts, bitmaps</td>
    </tr>
    <tr>
      <td><code>winmm</code></td>
      <td>Multimedia: timers, sound, joystick</td>
    </tr>
    <tr>
      <td><code>shell32</code></td>
      <td>Shell operations: file dialogs, launching apps</td>
    </tr>
    <tr>
      <td><code>ole32</code></td>
      <td>COM object support</td>
    </tr>
    <tr>
      <td><code>oleaut32</code></td>
      <td>Automation support for COM</td>
    </tr>
    <tr>
      <td><code>uuid</code></td>
      <td>GUID generation and COM identifiers</td>
    </tr>
</table>

Windows libraries location: C:\Program Files (x86)\Windows Kits\10\Lib\10.0.26100.0\um\x64

<h2>UCRT64 CMakePresets.json preset</h2>
<p>It was necessary because VCPKG_APPLOCAL_DEPS controls whether vcpkg runs a post-build PowerShell script (applocal.ps1) to copy runtime dependencies next to your binary. MSYS2 does not recognize powershell.</p>
<code> "VCPKG_APPLOCAL_DEPS": "OFF"</code>
<h3>using install</h3>
<code>cmake --install ./build/ucrt64-gcc</code>

<h2>Add VCPKG to terminal path</h2>
<code> $env:PATH += ";C:\vcpkg" </code>
<h3>Get path to vcpkg.exe</h3>
<code>Get-Command vcpkg</code>

<h2>install clarification</h2>
<p>vs code taskbar configuration only does configurations and build, NOT intall.  Install must be initiated via terminal, bash (gcc) or developer powershell (MSVC). Outputs just outputs but install installs, in order to maintain separtion</p>

### ucrt64-gcc install
```
cmake --install build/ucrt64-gcc
```

### MSVC install
```
cmake --install build/release --config Release
```
