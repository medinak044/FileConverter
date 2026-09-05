# File Converter Versioning Notes

## Current version

The current application version is **2.3.0**.

## Locations to update for a new version

When releasing a new version, update all of the following locations:

1. `version.xml`
   - Update the `<Latest Major="..." Minor="..." Patch="..." />` values.
   - Update the release URL to the correct GitHub release tag and installer filename.

2. `Application/FileConverter/Application.xaml.cs`
   - Update the `Application.Version` values (`Major`, `Minor`, and `Patch`).
   - This is the runtime version displayed by the application and used by upgrade checks.

3. `Application/FileConverter/Properties/AssemblyInfo.cs`
   - Update `AssemblyVersion`.
   - Update `AssemblyFileVersion`.

4. `Installer/Installer.wixproj`
   - Update `ProductVersion`.

5. `Installer/Product.wxs`
   - Update the WiX `<Package Version="..." />` value.

6. `CHANGELOG.md`
   - Add a new release section for the new version and document the changes.
   - Do not rewrite older historical release sections.

7. Search the repository for the previous version number before building.
   - Ignore `.git` and `.vs` metadata and unrelated numeric values such as codec quality values.
   - Confirm that all application and installer version references were updated.

## Build and installation verification

1. Close File Converter and any File Converter windows.
2. Build the installer using `Release` and `x64`:

   ```powershell
   cd E:\Scripts\FileConverter
   msbuild .\Installer\Installer.wixproj /restore /p:Configuration=Release /p:Platform=x64
   ```

3. Use the generated installer from:

   `Installer/bin/x64/Release/FileConverter-setup.msi`

4. **Uninstall the existing File Converter installation before testing a new development build.**
5. Restart Windows Explorer, or sign out and back in, so the shell extension is refreshed.
6. Install the newly generated MSI.
7. Start File Converter and verify that the application displays the new version.
8. If the old version is still displayed, uninstall again and reinstall the newly generated MSI. Also verify that the installed executable is from the new build rather than an older output folder.

## Installer signing

`Installer/Installer.wixproj` imports `Installer.sign` only when the file exists. Local builds can therefore produce an unsigned installer when private signing assets are unavailable. Do not distribute an unsigned installer publicly without appropriate code signing.
