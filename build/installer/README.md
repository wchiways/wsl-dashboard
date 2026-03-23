# WSL Dashboard Installer

## Overview
This module provides installer definitions for Windows:
- WiX MSI installer (`wix/Product.wxs`)
- NSIS installer (`nsis/installer.nsi`)

Common assets are stored in `common/`.

## Outputs
- MSI: `target/release/wsldashboard.v<version>.msi`
- NSIS: `target/release/wsldashboard.v<version>.nsis.exe`

## Inputs
- `common/app.ico`
- `common/LICENSE`
- `common/LICENSE.rtf`

## Build (local)
1. Build release binary:
   ```powershell
   cargo build --release
   ```
2. Prepare versioned exe:
   ```powershell
   $version = "X.Y.Z"
   Move-Item target/release/wsldashboard.exe target/release/wsldashboard.v$version.exe
   ```
3. Build MSI (WiX):
   ```powershell
   $version = "X.Y.Z"
   candle build/installer/wix/Product.wxs -arch x64 -dVersion=$version -dProductName="WSL Dashboard" -dManufacturer="WSL Dashboard" -dSourceExe="target/release/wsldashboard.v$version.exe" -dAppIcon="build/installer/common/app.ico" -dLicenseRtf="build/installer/common/LICENSE.rtf" -dLicenseFile="build/installer/common/LICENSE" -o build/installer/wix/
   light build/installer/wix/Product.wixobj -o target/release/wsldashboard.v$version.msi
   ```
4. Build NSIS:
   ```powershell
   $version = "X.Y.Z"
   $output_dir = "target/release"
   $source_exe = "target/release/wsldashboard.v$version.exe"
   $build_dir = "build/installer"
   & "${env:ProgramFiles(x86)}\NSIS\makensis.exe" /DVERSION=$version /DOUTPUT_DIR="$output_dir" /DSOURCE_EXE="$source_exe" /DBUILD_DIR="$build_dir" "build/installer/nsis/installer.nsi"
   ```
