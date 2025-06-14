# Pre-built Binaries

This directory contains pre-built binaries for different platforms to make installation easier.

## Windows

### Quick Start
```powershell
# Navigate to the Windows binary directory
cd bin/windows

# Run eks-node-viewer directly
.\eks-node-viewer.exe

# Or copy to your PATH
copy eks-node-viewer.exe C:\Windows\System32\
```

### Binary Information
- **Platform:** Windows AMD64
- **Version:** Built from latest source
- **Size:** ~72MB
- **Dependencies:** None (statically linked)

### Verification
```powershell
# Check version
.\eks-node-viewer.exe --version

# Test basic functionality
.\eks-node-viewer.exe --help
```

## Building from Source

If you prefer to build from source or need a different architecture:

### Windows
```powershell
.\build.ps1
```

### Linux/macOS
```bash
make build
```

## Notes

- Pre-built binaries are provided for convenience
- For production use, consider building from source
- Binaries are built with CGO disabled for maximum compatibility
- All binaries are statically linked with no external dependencies
