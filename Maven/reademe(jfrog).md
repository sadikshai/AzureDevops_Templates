# Maven Pipeline with JFrog Artifactory Integration

## Overview
This repository provides an Azure DevOps pipeline template designed for Java projects that use Maven and integrate with JFrog Artifactory. The pipeline supports dependency resolution, artifact deployment to Artifactory repositories, and publishing build metadata to Artifactory for traceability.

## Features
- **Artifactory Integration**: Facilitates dependency resolution and artifact deployment to JFrog Artifactory's release and snapshot repositories.
- **Build Metadata Publishing**: Automatically publishes build information, including build name and number, to Artifactory.
- **Dynamic Parameterization**: Supports customizable parameters for repository configuration, Artifactory services, and Maven build goals.
- **Reusable Template**: Offers a standardized and scalable pipeline template for consistent CI/CD workflows.

## Parameters
| Name                        | Type   | Default Value            | Description                                       |
|-----------------------------|--------|--------------------------|---------------------------------------------------|
| `artifactoryResolverService`| String | `JFROG_CLOUD`            | Service connection for resolving dependencies.    |
| `targetResolveReleaseRepo`  | String | `spring-libs-release`    | Release repository for dependency resolution.     |
| `targetResolveSnapshotRepo` | String | `spring-libs-snapshot`   | Snapshot repository for dependency resolution.    |
| `artifactoryDeployService`  | String | `JFROG_CLOUD`            | Service connection for deploying artifacts.       |
| `targetDeployReleaseRepo`   | String | `spring-libs-release`    | Release repository for artifact deployment.       |
| `targetDeploySnapshotRepo`  | String | `spring-libs-snapshot`   | Snapshot repository for artifact deployment.      |
| `artifactoryConnection`     | String | `JFROG_CLOUD`            | Service connection for publishing build metadata. |

## Pipeline Steps
1. **JFrog Maven Build and Artifact Management**  
   - Executes Maven goals (`install` by default) to build the project.
   - Resolves dependencies using JFrog Artifactory's specified release and snapshot repositories.
   - Deploys artifacts to JFrog Artifactory based on the build configuration.
   - Filters deployed artifacts to optimize deployment processes.

2. **Publish Build Metadata**  
   - Publishes build metadata, including the build name and number, to JFrog Artifactory for enhanced traceability.

3. **Reusable Template**  
   - Provides a flexible and reusable pipeline template for integrating Maven builds with JFrog Artifactory, ensuring consistency and scalability across projects.

## Usage
To use this pipeline:
1. Include the repository as a resource in your Azure DevOps project.
2. Use the `Maven/maven-jfrog.yml` template in your pipeline configuration.

Example:
```yaml
resources:
  repositories:
    - repository: Maven_template
      name: sadikshai/AzureDevops_Templates
      type: github
      ref: refs/heads/main
      endpoint: github.com_sadikshai

steps:
  - template: Maven/maven-jfrog.yml@Maven_template
    parameters:
      artifactoryResolverService: JFROG_CLOUD
      targetResolveReleaseRepo: spring-libs-release
      targetResolveSnapshotRepo: spring-libs-snapshot
      artifactoryDeployService: JFROG_CLOUD
      targetDeployReleaseRepo: spring-libs-release
      targetDeploySnapshotRepo: spring-libs-snapshot
      artifactoryConnection: JFROG_CLOUD
