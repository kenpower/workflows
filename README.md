# workflows
Shared workflows and actions

## Available Workflows

### Build Visual Studio C++ Project

A reusable workflow for building Visual Studio C++ projects using MSBuild.

#### Usage

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/build.yml`) with the following content:

```yaml
name: Build C++ Project

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    uses: kenpower/workflows/.github/workflows/build-vs-cpp.yml@main
    with:
      solution-path: 'path/to/your/solution.sln'
      configuration: 'Release'
      platform: 'x64'
```

#### Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `solution-path` | Path to the Visual Studio solution (.sln) or project (.vcxproj) file | Yes | - |
| `configuration` | Build configuration (e.g., Debug, Release) | No | `Release` |
| `platform` | Build platform (e.g., x64, Win32, ARM64) | No | `x64` |
| `msbuild-version` | MSBuild version to use (e.g., latest, 17.0, 16.0) | No | `latest` |
| `vs-version` | Visual Studio version (e.g., 2022, 2019) | No | `2022` |
| `build-args` | Additional MSBuild arguments | No | `''` |
| `enable-cache` | Enable caching of build artifacts | No | `true` |
| `run-tests` | Run tests after build | No | `false` |
| `test-executable` | Path to test executable (required if run-tests is true) | No | `''` |
| `upload-artifacts` | Upload build artifacts | No | `false` |
| `artifact-name` | Name for the uploaded artifact | No | `build-output` |
| `artifact-path` | Path to artifacts to upload | No | `''` |

#### Outputs

| Output | Description |
|--------|-------------|
| `build-status` | Build status (success or failure) |

#### Examples

##### Basic Build

```yaml
jobs:
  build:
    uses: kenpower/workflows/.github/workflows/build-vs-cpp.yml@main
    with:
      solution-path: 'MyProject.sln'
```

##### Build with Tests

```yaml
jobs:
  build:
    uses: kenpower/workflows/.github/workflows/build-vs-cpp.yml@main
    with:
      solution-path: 'MyProject.sln'
      configuration: 'Debug'
      platform: 'x64'
      run-tests: true
      test-executable: 'x64/Debug/MyTests.exe'
```

##### Build with Artifacts

```yaml
jobs:
  build:
    uses: kenpower/workflows/.github/workflows/build-vs-cpp.yml@main
    with:
      solution-path: 'MyProject.sln'
      configuration: 'Release'
      platform: 'x64'
      upload-artifacts: true
      artifact-name: 'my-app-release'
      artifact-path: 'x64/Release/*.exe'
```

##### Advanced Build with Custom MSBuild Arguments

```yaml
jobs:
  build:
    uses: kenpower/workflows/.github/workflows/build-vs-cpp.yml@main
    with:
      solution-path: 'MyProject.sln'
      configuration: 'Release'
      platform: 'x64'
      vs-version: '2019'
      build-args: '/p:PreferredToolArchitecture=x64 /p:UseMultiToolTask=true'
      enable-cache: true
```
