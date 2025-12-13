# Compli-AI

<div align="center">

[![PyPI version](https://badge.fury.io/py/compli-ai.svg)](https://badge.fury.io/py/compli-ai)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

**The "Terraform" for EU AI Compliance.** *Automate Annex IV Technical Documentation directly from your codebase.*

[Website](https://compli-ai.org) • [Documentation](https://github.com/compli-ai/compli-ai/wiki) • [Contributing](CONTRIBUTING.md)

</div>

---

## 🏛️ The Mission

**Compli-AI** is an open-source toolchain that treats **Compliance as Code**.

As AI regulations (EU AI Act, ISO 42001) tighten, engineering teams face a choice: slow down velocity to write Word documents, or face existential legal risk. Compli-AI bridges this gap by auto-generating technical documentation from your source code and maintaining a declarative "Compliance State File" (`compli.yaml`).

It is designed to be **Boring, Trusted, and Invisible**—integrating seamlessly into your CI/CD pipeline.

## ✨ Features

* **🔍 Zero-Config Discovery:** Automatically detects Hugging Face models, PyTorch architectures, and critical dependencies.
* **📄 Compliance-as-Code:** Generates a `compli.yaml` state file to track "Intended Purpose" and "Risk Category" alongside your code.
* **🇪🇺 EU AI Act Ready:** Standardized templates mapped directly to **Annex IV** requirements.
* **🛡️ Privacy First:** Runs 100% locally. No code or data ever leaves your machine.
* **🧼 Signal-Only:** Smart filtering ignores standard library modules (`os`, `json`) to produce clean, auditor-ready Bills of Materials (SBOMs).

## 🚀 Quick Start

### 1. Installation

```bash
pip install compli-ai
```

### 2. Initialize Governance

Navigate to your AI project root and run the initialization command. This scans your code and creates your compliance state file.

```bash
cd my-ai-project
compli-ai init
```

### 3. Configure Policy

Open the generated `compli.yaml`. The tool will have auto-filled the technical details (models, dependencies). Your job is to declare the **Intent**.

```yaml
# compli.yaml

policy:
  # EU AI Act Annex IV (2)(b)
  intended_purpose: "Classify customer support tickets for routing."
  
  # EU AI Act Title III
  risk_category: limited_risk
```

### 4. Continuous Scanning

Run the scanner in your CI/CD pipeline to detect "Drift" (e.g., a developer adds a new high-risk model without updating the policy).

```bash
compli-ai scan .
```

## 🏗️ Architecture

Compli-AI follows the "Switzerland" philosophy: Neutral, precise, and secure.

* **Inspector Engine:** Uses Python's Abstract Syntax Tree (AST) to parse code without executing it.
* **State Management:** The `compli.yaml` file acts as the single source of truth for compliance metadata.
* **Output:** Generates human-readable tables for developers and JSON/Markdown for auditors.

## 🤝 Contributing

We welcome contributions to help standardize AI governance. Please see our [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## ⚖️ License

Copyright © 2025 Compli-AI.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
