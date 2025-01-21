# .NET Pipeline with Conditional Test Execution

## Overview
This repository contains an Azure DevOps pipeline template for building, testing, and publishing .NET projects. The pipeline supports dynamic parameterization, allowing flexible configurations such as skipping tests, specifying versions, and customizing project paths.

## Features
- **Conditional Builds Based on Version**: Builds projects based on whether a specific version is mentioned.
- **Optional Test Execution**: Enables skipping or executing tests based on the `RunTests` parameter.
- **Artifact Publishing**: Publishes compiled DLLs and outputs in a structured manner for deployment or sharing.
- **Reusable Template**: Provides a parameterized template for consistent CI/CD workflows across multiple .NET projects.

## Parameters
| Name               | Type    | Default Value                         | Description                                             |
|--------------------|---------|---------------------------------------|---------------------------------------------------------|
| `mainproject`      | String  | `**/*.csproj`                         | Path to the main .NET project(s) to build.              |
| `Testproject`      | String  | `**/*Tests.csproj`                    | Path to the test project(s) for execution.              |
| `RunTests`         | Boolean | `true`                                | Flag to enable or skip test execution.                  |
| `specificversion`  | String  | `' '`                                 | Specifies a version for the build; defaults to none.    |

## Pipeline Steps
1. **Build Main Project**
   - Builds the main project(s) using the specified `.csproj` file(s).
   - Handles version-specific builds with conditional logic.

2. **Execute Tests (Optional)**
   - Executes tests in the specified test project(s) if the `RunTests` parameter is `true`.

3. **Publish Project**
   - Publishes the main project to a specified directory with additional options like zipping output and modifying paths.

4. **Copy and Publish Artifacts**
   - Copies compiled DLLs to the build artifact staging directory.
   - Publishes build artifacts for further use or deployment.

5. **Reusable Template**
   - Allows users to customize project paths, test execution, and build conditions for different projects by extending the template.

## Usage
To use this pipeline:
1. Include this repository as a resource in your Azure DevOps project.
2. Use the `Dotnet/dotnet-pipeline.yml` template in your pipeline configuration.

Example:
```yaml
extends:
  template: 'Dotnet/dotnet-pipline.yml@Dotnet_Template'
parameters:
  mainproject: 'src/Presentation/Nop.Web/Nop.Web.csproj'
  Testproject: 'src/Tests/Nop.Tests/Nop.Tests.csproj'
  RunTests: false
  specificversion: '5.0'
