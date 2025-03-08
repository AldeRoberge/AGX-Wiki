Semantic Versioning ([SemVer](https://semver.org/)) follows the format `MAJOR.MINOR.PATCH`, where each part represents different levels of changes:

- **MAJOR**: Breaking changes (changes that are not backward-compatible).  
- **MINOR**: New features in a backwards-compatible way.  
- **PATCH**: Backwards-compatible bug fixes.  

When releasing pre-release packages, a pre-release label is added after the version number to indicate that the software is not stable and is still under development.  

The format for pre-release versions is:  
`MAJOR.MINOR.PATCH-PRERELEASE`

## Common Pre-release Labels  

### Alpha (`alpha`)
- **Description**: Early versions, typically unstable, incomplete features, and used for internal testing or initial development.  
- **Example**: `1.0.0-alpha.1` (First alpha release).  

### Beta (`beta`)
- **Description**: More stable than alpha, but still not fully stable. Often released for external testing and feedback.  
- **Example**: `1.0.0-beta.2` (Second beta release).  

### Release Candidate (`rc`)
- **Description**: A pre-release that is nearly production-ready but still requires final testing. If no issues arise, it becomes the stable release.  
- **Example**: `1.0.0-rc.1` (First release candidate).  

### Preview (`preview`)
- **Description**: A version close to feature-complete but still undergoing final testing. More stable than alpha or beta.  
- **Example**: `1.0.0-preview.3` (Third preview release).  

### Nightly (`nightly`)
- **Description**: Built daily from the latest code, may be unstable. Often used for continuous integration testing.  
- **Example**: `1.0.0-nightly.20230218` (Nightly build from February 18, 2023).  

### Development (`dev`)
- **Description**: Represents ongoing development and is typically unstable. Often tied to a specific development branch.  
- **Example**: `1.0.0-dev.4` (Fourth development version).  

### Experimental (`experimental`)
- **Description**: Versions containing experimental features or untested code, usually unstable.  
- **Example**: `1.0.0-experimental.1` (First experimental version).  

### Snapshot (`snapshot`)
- **Description**: A specific point in development, usually unstable.  
- **Example**: `1.0.0-snapshot.20230218` (Snapshot from February 18, 2023).  

### Hotfix (`hotfix`)
- **Description**: Quick fixes for production issues, often released as part of the PATCH version.  
- **Example**: `1.0.0-hotfix.1` (First hotfix release).  

## Multiple Pre-release Labels  
Pre-release labels can be combined to indicate more specific stages of development, though this is less common:  

- **Example**: `1.0.0-alpha.2-beta.3` (Alpha release with some beta-level changes).  
- **Example**: `1.0.0-rc.1-nightly-20230218` (Release candidate built from a nightly version on February 18, 2023).  

## Pre-release Label Summary  

| Label         | Description                                      | Example                       |
|--------------|------------------------------------------------|-------------------------------|
| `alpha`      | Early, unstable version.                        | `1.0.0-alpha.1`               |
| `beta`       | More stable, for external testing.              | `1.0.0-beta.2`                |
| `rc`         | Release candidate, nearly production-ready.     | `1.0.0-rc.1`                  |
| `preview`    | Feature-complete but final testing.             | `1.0.0-preview.3`             |
| `nightly`    | Built from latest code, daily unstable version. | `1.0.0-nightly.20230218`      |
| `dev`        | Ongoing development, usually unstable.          | `1.0.0-dev.4`                 |
| `experimental` | Contains experimental or untested features.   | `1.0.0-experimental.1`        |
| `snapshot`   | A specific point in ongoing development.        | `1.0.0-snapshot.20230218`     |
| `hotfix`     | Critical bug fixes, usually part of a patch.    | `1.0.0-hotfix.1`              |

## Purpose of Pre-release Labels  
- **Clarity**: Pre-release labels give users insight into the stage of development and whether they can rely on the version for production use.  
- **User Expectations**: Labels help set expectations about stability, making sure users know the software may not be stable enough for production.  
- **Encouraging Feedback**: Pre-releases are designed to gather feedback from testers, enabling further improvements before the final stable release.  

## Conclusion  
Semantic Versioning (SemVer) provides a clear and structured way to version pre-release software with labels like alpha, beta, rc, preview, and more. By using these labels, developers can better manage the release cycle and ensure that users understand the stability and intended usage of each version.  

---

# Branches  

### **Main (or master)**  
- Typically holds the stable production-ready code. When a release is ready for production, it’s tagged from this branch.  

### **Develop**  
- Holds the latest development changes. This branch often contains feature updates that are tested and can transition between pre-release stages like alpha, beta, and release candidate. Versions are tagged as alpha (e.g., `1.0.0-alpha.1`).  

### **Feature Branches**  
- Used for specific new features. These are merged into the develop branch, which triggers the pipeline for testing, versioning, and pre-release generation. Feature branches don’t directly affect the versioning; it's the merge into develop that triggers versioning.  

> **Feature branches don’t trigger a build.** Merging into `dev` triggers tests to be run, an artifact to be created, and published to the servers.

---

# Release Phases  

## 1. **During Alpha (Early Development)**  
- **Main Focus**: New features and functionality are being added.  
- **Development Continuation**: Ongoing, with regular code changes and experimental features.  
- **Testing**: Automated unit tests and integration tests run as part of CI. Bugs are fixed, but the focus remains on new functionality.  

## 2. **During Beta (Stabilization Phase)**  
- **Main Focus**: The codebase is feature-complete, but efforts shift toward bug fixes, performance improvements, and stability.  
- **Development Slows**: Developers focus more on polishing and fixing bugs rather than introducing major new features.  
- **Testing**: Intensive testing, including manual and beta testing with external users.  

## 3. **During Final Release (Stable Production Version)**  
- **Main Focus**: Ensuring the code is stable and production-ready.  
- **Minor Development & Hotfixes**: New features are avoided, but critical hotfixes may be deployed.  
- **Post-Release Maintenance**: Bug fixes and minor optimizations continue as patches or minor updates.  

---

# Summary of Release Stages  

- **Alpha**: Initial phase, incomplete features, many bugs, internal testing.  
- **Beta**: More stable, external testing, feedback collection.  
- **Release Candidate (RC)**: Almost final version, minimal bugs, last round of testing.  
- **General Availability (GA)**: Official, stable release available to the public.  
