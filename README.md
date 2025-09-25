<h2> create system link to allow MSYS UCRT64 to recognize c:\vcpkg </h2> 
<p>from ucrt64 bash</p>
<code>
mkdir -p /usr/local/bin</br>
ln -s /c/vcpkg/vcpkg.exe /usr/local/bin/vcpkg </br>
export VCPKG_ROOT=/c/vcpkg  
</code>
<h2>make VCPKG_ROOT persistent</h2>
<code>
echo 'export VCPKG_ROOT=/c/vcpkg' >> ~/.bashrc</br>
</code>
<h2>generate and then build ucrt64-release</h2>
<p>from ucrt64 bash $</p>
<code>  
rm -rf build/ucrt64-gcc</br>
cmake --preset ucrt64-gcc</br>
cmake --build --preset ucrt64-gcc</br>
</code><br>
<h2> Add PowerShell to MSYS2 $PATH </h2>  
Bash<br>
<code>
export PATH="/c/Windows/System32/WindowsPowerShell/v1.0:$PATH"
</code>

<h2>Common Windows Libraries</h2>
<table>
  <thead>
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

<p>Windows libraries location: C:\Program Files (x86)\Windows Kits\10\Lib\10.0.26100.0\um\x64 </p>