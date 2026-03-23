# Installer Design

## Goals
- Produce MSI and NSIS installers for x64.
- Use existing app icon and license.
- Create Start Menu and Desktop shortcuts.
- Support upgrades via stable UpgradeCode (MSI).

## Components
### WiX (MSI)
- Product metadata: Name, Manufacturer, Version.
- Upgrade: MajorUpgrade with stable UpgradeCode.
- Install directory: `ProgramFiles64Folder\wsl-dashboard`.
- Files: `wsldashboard.exe`, `LICENSE`.
- Shortcuts: Start Menu + Desktop.

### NSIS
- Install directory: `$PROGRAMFILES64\wsl-dashboard`.
- Files: `wsldashboard.exe`, `LICENSE`.
- Shortcuts: Start Menu + Desktop.
- Uninstall entry: HKLM `Software\Microsoft\Windows\CurrentVersion\Uninstall`.

## Assets
- `common/app.ico`
- `common/LICENSE`
- `common/LICENSE.rtf`

## Release Integration
GitHub Actions builds:
- `wsldashboard.v<version>.exe`
- `wsldashboard.v<version>.msi`
- `wsldashboard.v<version>.nsis.exe`

These are uploaded as release assets.
