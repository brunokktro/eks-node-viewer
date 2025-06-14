# Windows Setup Guide for eks-node-viewer

This guide provides comprehensive instructions for installing and using eks-node-viewer on Windows systems.

## Quick Start

### Method 1: Pre-built Binary (Recommended)

1. **Download the latest release:**
   - Go to [GitHub Releases](https://github.com/awslabs/eks-node-viewer/releases)
   - Download the Windows binary (`eks-node-viewer-windows-amd64.zip`)

2. **Extract and run:**
   ```powershell
   # Extract the ZIP file
   Expand-Archive -Path eks-node-viewer-windows-amd64.zip -DestinationPath . -Force
   
   # Run the tool
   .\eks-node-viewer.exe
   ```

3. **Verify installation:**
   ```powershell
   .\eks-node-viewer.exe --version
   ```

### Method 2: Build from Source

> **Note:** Building from source requires Go installation and takes several minutes to download dependencies. Most users should use the pre-built release above.

**Prerequisites:**
- Go 1.21 or later
- Git

**Install Go using Chocolatey:**
```powershell
# Install Chocolatey (if not already installed)
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install Go
choco install golang -y

# Close and reopen PowerShell, then verify
go version
```

**Build using PowerShell script:**
```powershell
# Clone the repository
git clone https://github.com/awslabs/eks-node-viewer.git
cd eks-node-viewer

# Build using PowerShell script
.\build.ps1

# Or build with tests
.\build.ps1 -Test
```

**Manual build:**
```powershell
# Set environment variables
$env:CGO_ENABLED = "0"
$env:GOOS = "windows"
$env:GOARCH = "amd64"

# Build
go build -ldflags="-s -w" -o eks-node-viewer.exe ./cmd/eks-node-viewer
```

## Usage Examples

### Basic Usage
```powershell
# Standard usage
.\eks-node-viewer.exe

# With AWS profile and region
$env:AWS_PROFILE = "myprofile"
$env:AWS_REGION = "us-west-2"
.\eks-node-viewer.exe
```

### Advanced Usage
```powershell
# Karpenter nodes only
.\eks-node-viewer.exe --node-selector karpenter.sh/nodepool

# Display both CPU and Memory Usage
.\eks-node-viewer.exe --resources cpu,memory

# Display extra labels (AZ)
.\eks-node-viewer.exe --extra-labels topology.kubernetes.io/zone

# Sort by CPU usage in descending order
.\eks-node-viewer.exe --node-sort=eks-node-viewer/node-cpu-usage=dsc

# Disable pricing (faster startup)
.\eks-node-viewer.exe --disable-pricing
```

## Windows-Specific Features

### PowerShell Integration
- Native PowerShell build script (`build.ps1`)
- Colored output and progress indicators
- Windows-specific error handling

### Windows Terminal Support
- Enhanced Unicode rendering
- Improved color support
- Better terminal integration

## Troubleshooting

### Common Issues

#### "eks-node-viewer is not recognized as an internal or external command"
- Ensure you're using `.\eks-node-viewer.exe` (with `.\` prefix)
- Or add the directory to your PATH environment variable

#### Build Issues
```powershell
# Clean and rebuild
.\build.ps1 -Clean
.\build.ps1
```

#### Go Installation Issues
```powershell
# Verify Go installation
go version

# If not found, reinstall Go
choco install golang -y --force
```

### AWS Configuration

Ensure your AWS credentials are configured:
```powershell
# Check AWS CLI configuration
aws configure list

# Or set environment variables
$env:AWS_ACCESS_KEY_ID = "your-access-key"
$env:AWS_SECRET_ACCESS_KEY = "your-secret-key"
$env:AWS_REGION = "us-west-2"
```

### Performance Tips

1. **Disable pricing for faster startup:**
   ```powershell
   .\eks-node-viewer.exe --disable-pricing
   ```

2. **Use specific node selectors:**
   ```powershell
   .\eks-node-viewer.exe --node-selector karpenter.sh/nodepool
   ```

3. **Limit displayed resources:**
   ```powershell
   .\eks-node-viewer.exe --resources cpu
   ```

## Development

### Building with Different Options

```powershell
# Build with version info
.\build.ps1 -Version "1.0.0"

# Build and run tests
.\build.ps1 -Test

# Clean build
.\build.ps1 -Clean

# Generate code and build
.\build.ps1 -Generate
```

### Testing

```powershell
# Run all tests
go test ./...

# Run tests with coverage
go test -cover ./...

# Run specific test
go test ./pkg/model
```

## Support

For Windows-specific issues:
1. Check this documentation first
2. Verify Go and AWS CLI installation
3. Try building from source if binary doesn't work
4. Open an issue with Windows-specific details

For general eks-node-viewer issues, please refer to the main [README](README.md) and open an issue on GitHub.
