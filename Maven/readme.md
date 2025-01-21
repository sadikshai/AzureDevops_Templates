# Maven Pipeline for Java Projects

## Overview
This repository contains a reusable Azure DevOps pipeline for building, testing, and publishing Java projects using Maven. The pipeline supports dynamic parameterization, custom JDK versions, and artifact management.

## Features
- **Dynamic Parameterization**: Easily customize build goals, test result paths, and artifact paths.
- **Conditional Execution**: Switch between specific JDK versions or default settings.
- **Artifact Management**: Copies and publishes JAR artifacts for deployment or further use.
- **Reusable Templates**: Includes templates for efficient pipeline management and consistency across multiple projects.

## Parameters
| Name               | Display Name       | Type   | Default Value                   | Description                               |
|--------------------|--------------------|--------|---------------------------------|-------------------------------------------|
| `goal`             | `build`           | String | `clean package`                | Specifies Maven goals to execute.         |
| `testResultsFiles` | `testfile`         | String | `**/surefire-reports/TEST-*.xml`| Path for test result files.               |
| `specificversion`  | `jdkVersion`       | String | `' '`                           | JDK version to use; defaults to system JDK.|
| `acrtifactpath`    | `pathforartifact` | String | `**/*.jar`                      | Path to JAR artifacts.                    |

## Pipeline Steps
1. **Build and Test with Maven**  
   Executes Maven goals defined in the parameters and publishes JUnit test results. Conditional logic handles JDK version specification.
2. **Copy Artifacts**  
   Copies the JAR files matching the specified pattern to the build artifact staging directory.
3. **Publish Artifacts**  
   Publishes the staged artifacts as build outputs for deployment or sharing.

## Usage
To integrate this pipeline into your Azure DevOps project:
1. Include this repository as a resource in your pipeline definition.
2. Use the `extends` keyword to reference the `maven-pipeline.yml` template.
3. Pass required parameters to the pipeline.

Example:
```yaml
extends:
  template: 'Maven/maven-pipeline.yml@Maven_Template'
parameters:
  goal: clean package
  testResultsFiles: '**/surefire-reports/TEST-*.xml'
  specificversion: '11'
  acrtifactpath: '**/*.jar'
