# Comment on PR with Structurizr Diagrams Action

## Introduction

This GitHub Action, designed to complement the [Generate Structurizr Diagrams Images from DSL](https://github.com/marketplace/actions/generate-structurizr-diagrams-images-from-dsl) action, automatically comments on pull requests with the previously generated Structurizr diagrams. It ensures that team members can easily review the latest architecture diagrams directly within the context of a PR.

## Prerequisites

To use this action effectively, you should have:

- A GitHub repository.
- Completed the setup of the "Generate Structurizr Diagrams Images from DSL" action in your repository.
  
## Usage

This action is meant to be used in a separate workflow that triggers after the "Generate Structurizr Diagrams Images from DSL" workflow. To set it up:

1. **Create a workflow file**: In your repository's `.github/workflows` directory, create a new file (e.g., `structurizr-diagrams-comment.yml`) with the following content:

```yaml
name: Comment on PR with Structurizr Diagrams

on:
    workflow_run:
        types:
            - completed
        workflows:
            - "Update Structurizr Diagrams"

jobs:
    comment-on-pr:
        if: github.event.workflow_run.conclusion == 'success'
        runs-on: ubuntu-latest
        steps:
        - uses: sebastienfi/structurizr-pr-comment@v1
```

## How It Works

- The action triggers after the "Update Structurizr Diagrams" workflow completes.
- It retrieves information about the PR and lists the generated diagram files.
- If diagrams are updated, the action posts or updates a comment in the PR with the diagrams.

## Contributing

Contributions to improve this action are welcome. Ensure your contributions are well-documented and follow the coding standards of this project.
