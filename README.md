# Jenkins Pipeline for Branch Deployment

This repository contains a Jenkins pipeline script designed to deploy specific branches to a remote server using SSH. The pipeline allows for dynamic branch selection and provides detailed feedback during execution.

---

## Features

- **Dynamic Branch Selection**: Allows the user to specify the branch to deploy through a pipeline parameter.
- **Build Information Display**: Captures and displays key build details, including the branch being deployed and the user who triggered the build.
- **Remote Deployment via SSH**: Executes a deployment script on a remote server using SSH.
- **Error Handling**: Validates SSH command execution and provides meaningful error messages in case of failures.

---

## Pipeline Overview

The pipeline is divided into two main stages:

### 1. **Build Info**
- Captures details about the build trigger, including the user who initiated it.
- Updates the build display name in Jenkins with relevant information:
  - Build number
  - Branch being deployed
  - User who triggered the build

### 2. **Deploy**
- Executes a remote deployment script via SSH, passing the selected branch as a parameter.
- Validates the result of the SSH command.
- Catches and handles exceptions to ensure proper error reporting.

---

## Prerequisites

1. **Jenkins Setup**:
   - A Jenkins instance with the ability to execute pipelines.
   - The SSH key of the Jenkins user added to the remote server's authorized keys.

2. **Remote Server**:
   - The server should have the deployment script (`deploy.sh`) available and executable.
   - The script should support branch deployment. For example:
     ```bash
     #!/bin/bash
     BRANCH=$1
     echo "Deploying branch: $BRANCH"
     git checkout $BRANCH
     git pull origin $BRANCH
     # Add deployment steps here
     ```

---

## Usage

### Pipeline Parameters
The pipeline requires the following parameter:
- **BRANCH**: The name of the branch to deploy.

### Example Execution
1. Trigger the pipeline in Jenkins.
2. Enter the branch name (e.g., `main`, `feature-xyz`) in the `BRANCH` parameter field.
3. Observe the build progress and results in the Jenkins console output.

---

## Script Details

---

## Error Handling

1. **SSH Command Validation**:
   - Ensures the deployment script on the remote server executed successfully.
   - Provides an error message if the command returns a non-zero exit code.

2. **Exception Handling**:
   - Captures exceptions during pipeline execution and reports them with detailed messages.

---

## Contributing

Feel free to submit issues or pull requests for improvements to the pipeline.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
