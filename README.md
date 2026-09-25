# Forge downloads

Public, source-free downloads of the Forge command-line tool (Windows x64 and Linux x64) and the
Forge Process Metrics VS Code extension. No access to the private source repository is needed.

Download a specific version from [Releases](https://github.com/jjolliff/forge-downloads/releases)
when you need a reproducible install. The examples below use the latest release.

## Windows: Forge CLI

In PowerShell:

```powershell
$base = 'https://github.com/jjolliff/forge-downloads/releases/latest/download'
curl.exe -fL "$base/forgeWindowsX64.zip" -o forgeWindowsX64.zip
curl.exe -fL "$base/sha256.txt" -o sha256.txt
Get-FileHash forgeWindowsX64.zip -Algorithm SHA256
# Compare the hash with the forgeWindowsX64.zip line in sha256.txt before extracting.
Expand-Archive forgeWindowsX64.zip -DestinationPath "$HOME\tools\forge" -Force
& "$HOME\tools\forge\forge.exe" --help
```

The ZIP contains `forge.exe`; no installer or clone is required. Add `$HOME\tools\forge` to your
`PATH` only if you want to invoke `forge` without its full path.

## Linux: Forge CLI

```bash
base=https://github.com/jjolliff/forge-downloads/releases/latest/download
curl -fL "$base/forgeLinuxX64.tar.gz" -o forgeLinuxX64.tar.gz
curl -fL "$base/sha256.txt" -o sha256.txt
grep ' forgeLinuxX64.tar.gz$' sha256.txt | sha256sum -c -
mkdir -p "$HOME/.local/bin"
tar -xzf forgeLinuxX64.tar.gz -C "$HOME/.local/bin"
"$HOME/.local/bin/forge" --help
```

The tarball contains a statically linked `forge` executable. Add `$HOME/.local/bin` to `PATH` if
needed. Some commands, such as `forge format`, also need external tools (for example clang-format
23.1.1); `forge --help` lists the available commands.

## VS Code: Process Metrics

Download [forge-metrics.vsix](https://github.com/jjolliff/forge-downloads/releases/latest/download/forge-metrics.vsix)
and install it in VS Code with **Extensions: Install from VSIX...**, then reload the window. Or run:

```powershell
code --install-extension .\forge-metrics.vsix
```

The extension shows CPU and resident memory for a *locally launched debuggee* while a VS Code
debug session is running. Use **Forge Metrics: Show Process Metrics** to open its history panel.
It does not measure the whole machine or watch programs started outside the debugger. If your
debugger does not report a local process ID, use **Forge Metrics: Select Debuggee PID** during the
session. You can compare the VSIX's SHA-256 with its entry in
[sha256.txt](https://github.com/jjolliff/forge-downloads/releases/latest/download/sha256.txt).
