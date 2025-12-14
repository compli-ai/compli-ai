# Contributing to Compli-AI

Thank you for your interest in contributing to Compli-AI! We are building the open standard for AI compliance, and we value robust, well-tested code.

## 🏛️ Guiding Principles

* **Boring but Trusted:** We prioritize stability and correctness over new features.
* **Compliance as Code:** All features must support the goal of making compliance declarative and auditable.
* **Privacy First:** All analysis runs locally. User source code is never transmitted. No data leaves the machine without an explicit command.

## 🛠️ Development Setup

This project uses [Poetry](https://python-poetry.org/) for dependency management.

1.  **Fork and Clone** the repository.
2.  **Install Dependencies:**
    ```bash
    poetry install
    ```
3.  **Run Tests:**
    ```bash
    poetry run pytest
    ```

## 📝 Pull Request Process

1.  **Strict Typing:** We use `mypy` for static type checking. Please ensure your code is fully typed.
2.  **Formatting:** We follow the standard Python style.
3.  **Commit Messages:** Please use descriptive commit messages (e.g., `feat: add support for keras models` or `fix: ignore stdlib in dependency scan`).
4.  **Documentation:** If you change behavior, please update the README or the `compli.yaml` template comments.

## 🐛 Reporting Issues

Please use the GitHub Issues tab to report bugs. Include your python version, OS, and a reproduction snippet.

## 📜 License

By contributing, you agree that your code will be licensed under the Apache 2.0 License.

