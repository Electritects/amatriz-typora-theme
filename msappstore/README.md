# Microsoft Store Distribution Package

This directory is designated for Microsoft Store upload assets, release packages, and submission manifests:
- **Package Binaries**: Signed or upload-ready application packages (`.msix`, `.msixupload`, `.appxupload`).
- **Certification & Reports**: Windows App Certification Kit (WACK) validation reports (`.xml`, `.json`, `.log`).
- **Store Submission Metadata**: Submission manifests, package validation checksums, and store listing configurations.

> **Repository Architecture Policy**:
> - `coding/`: Strictly reserved for application source code.
> - `dist/`: Reserved for local unpackaged binaries, developer debug builds, and internal artifacts.
> - `msappstore/`: Dedicated to external Microsoft Store release packages and submission manifests.
