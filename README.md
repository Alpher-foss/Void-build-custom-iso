---

# Generating and Releasing ISO with GitHub Actions

Automate the process of generating and releasing an ISO for your project using GitHub Actions. This workflow is triggered by version tags and can also be manually initiated.

## Setup

### Repository Setup

Ensure your repository contains the following shell scripts:

- `set_repository.sh`
- `install_dependencies.sh`
- `gen.sh`

These scripts should handle setting up the environment, installing dependencies, and generating the ISO.

### GitHub Secrets

Add a secret named `PERSONAL_GITHUB_TOKEN` to your repository's secrets. This token will be used to authenticate and upload the ISO as a release asset.

### Workflow Configuration

Copy the provided YAML file and place it in the `.github/workflows` directory of your repository.

## Resolving "Resource not accessible by integration" Error

This error typically occurs when the GitHub token lacks the necessary permissions. To resolve this:

1. **Ensure Proper Permissions for `GITHUB_TOKEN`:**
   - Verify that the `secrets.GITHUB_TOKEN` has the correct permissions in the repository settings.

2. **Use a Personal Access Token (PAT):**
   - Create a PAT with the required scopes (e.g., `repo`, `workflow`).
   - Add this PAT as a secret in your repository, named `PERSONAL_GITHUB_TOKEN`, and use it in the workflow.

### Steps to Create a Personal Access Token

1. Go to [GitHub Settings](https://github.com/settings/tokens).
2. Click **Generate new token**.
3. Name the token and select the appropriate scopes (e.g., `repo`, `workflow`).
4. Generate the token and copy it.
5. Go to your repository's settings.
6. Navigate to **Secrets and variables** > **Actions**.
7. Add a new repository secret named `PERSONAL_GITHUB_TOKEN` and paste the token.

## Running the Workflow

### Triggering the Workflow

- The workflow is automatically triggered when a version tag is pushed to the repository.
- It can also be manually triggered through the GitHub Actions interface.

### Workflow Execution

1. **Generate ISO:**
   - The `gen_iso` job generates the ISO and uploads it as an artifact.
   
2. **Create Release:**
   - The `release` job creates a release and uploads the ISO as a release asset.

## Accessing the Generated ISO

Once the workflow is executed, the generated ISO can be downloaded from the release assets of the repository.

---
