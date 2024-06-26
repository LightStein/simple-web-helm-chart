# Helm Chart for Simple Web Application

This repository contains the Helm chart for the `simple-web` application, designed for deployment on Kubernetes within the `thomas` namespace.

## Environment

- Kubernetes cluster
- Helm 3.x

### Setup

- [x] **Repository Initialization**: Initialize and configure the Helm chart repository.
- [x] **Clone Repository**: Clone the repository to begin development.

### Helm Chart Development

- [x] **Create Chart Structure**: Establish the base structure of the Helm chart.
- [x] **Define Dependencies**: Add any required dependencies.

### Chart Components

- [x] **Deployment Template**: Craft the deployment specifications.
- [x] **Service Template**: Outline the service access points.
- [x] **Ingress Template**: Set up routing via ingress.
- [x] **KEDA Autoscaler Template**: Configure autoscaling settings.

### Configuration and Defaults

- [x] **Parameterize Chart**: Ensure all configurations are adjustable via `values.yaml`.
- [x] **Default Values**: Set default values for essential configuration items.

### Testing and Validation

- [x] **Lint Chart**: Check the chart for errors with `helm lint`.
- [x] **Dry Run Install**: Test installation configurations with a dry run.
- [x] **Install Chart**: Deploy the chart to a test environment.

### Documentation

- [x] **README File**: Document the deployment and configuration process.
- [ ] **Comments in Templates**: Provide clear comments in template files.

### Versioning and Releases

- [x] **Update Chart Version**: Update the version information for each significant change.

### Continuous Integration

- [x] **Setup CI Pipeline**: Implement a pipeline for automated testing and deployment.

## How to Use

To deploy the `simple-web` application using this Helm chart, navigate to the cloned repository directory and run:

```bash
helm install simple-web . --namespace thomas
