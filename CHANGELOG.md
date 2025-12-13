# Changelog

All notable changes to this project will be documented in this file.

## [0.2.0] - 2025-12-13

### Features
- **Compliance as Code**: Introduced the `compli-ai init` command to generate a `compli.yaml` file, establishing a new workflow for managing compliance documentation directly within a project.
- **Auto-Detection**: The `init` command automatically scans the codebase to populate the `system` section of `compli.yaml` with detected AI models and software dependencies.

### Fixes
- **Improved Model Detection**: The scanner can now detect Hugging Face models loaded via the `transformers.pipeline()` function, in addition to the `from_pretrained()` method.
