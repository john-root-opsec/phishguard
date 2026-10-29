# 🛡️ PHISHGUARD
### Intelligent URL Analysis & Phishing Threat Detection

**A desktop application for URL analysis, suspicious indicator identification, and investigation support for potential phishing threats.**

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PySide6-Desktop%20UI-41CD52?style=for-the-badge&logo=qt&logoColor=white" alt="PySide6">
  <img src="https://img.shields.io/badge/Domain-Cybersecurity-DC2626?style=for-the-badge" alt="Cybersecurity">
  <img src="https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-52525B?style=for-the-badge" alt="Platforms">
  <img src="https://img.shields.io/badge/Status-In%20Development-F59E0B?style=for-the-badge" alt="Development status">
</p>

---

## 📌 About the Project

**PHISHGUARD** is a Python-based desktop application focused on URL analysis and the identification of potential indicators associated with phishing attacks.

The project aims to bring multiple technical checks into a single graphical interface, allowing users to investigate suspicious URLs, understand analysis results, and review previous records.

Its goal is to transform technical checks that might otherwise require separate tools and commands into a more accessible, organized, and intuitive workflow.

PHISHGUARD is being developed as a practical project focused on **defensive cybersecurity, threat analysis, Python automation, and desktop application development**.

## 🎯 Project Objectives

- 🔎 **URL Analysis:** Examine URL characteristics and identify potentially suspicious patterns.
- 🧩 **Indicator Correlation:** Organize technical evidence to support URL assessments.
- 🌐 **Domain Investigation:** Integrate DNS and domain registration information when queries and data sources are available.
- 🔐 **TLS Checks:** Evaluate information related to a domain's secure connection.
- 🧠 **Result Explanations:** Help users understand the indicators identified during analysis.
- 📊 **History and Reports:** Support reviewing previous analyses and exporting results in JSON format.
- 🖥️ **Graphical Interface:** Provide application features through a desktop interface, reducing reliance on terminal commands.

## ⚙️ Features

| Feature | Description |
|---|---|
| URL Analysis | Evaluate URL characteristics and suspicious indicators. |
| Indicator Correlation | Organize relevant signals to support analysis. |
| DNS Lookup | Retrieve DNS information, depending on the available implementation. |
| RDAP | Retrieve domain registration information through supported RDAP queries. |
| Reputation Analysis | Provide a module for evaluating reputation-related information. |
| TLS Checks | Examine information related to TLS security. |
| AI-Assisted Explanations | Help interpret analysis results. |
| Analysis History | Store and review previous analyses. |
| JSON Reports | Organize results in a structured data format. |
| Desktop Interface | Navigate between dashboards, indicators, history, reports, and settings. |

> **Note:** The availability and depth of each check depend on the active implementation, configured data sources, and external services. The presence of a module does not necessarily mean that every integration is enabled.

## 🧠 How It Works

The PHISHGUARD analysis workflow can be represented through the following stages:

1. **Input:** The user submits a URL for investigation.
2. **Analysis:** The application examines URL characteristics and runs the implemented checks.
3. **Indicator Collection:** Specific modules may retrieve DNS, domain, TLS, and reputation-related information.
4. **Correlation:** Available indicators are organized to support interpretation.
5. **Presentation:** The interface displays analysis results and relevant information.
6. **Storage and Export:** When supported, results can be reviewed in the history and exported as JSON.

```text
                 ┌─────────────────────┐
                 │     URL Input       │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    URL Analysis     │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Technical Indicators│
                 │ DNS • RDAP • TLS    │
                 │ Reputation          │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Correlation & Review│
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Interface & Reports │
                 └─────────────────────┘
```

*Conceptual representation of the analysis workflow. The execution of each stage depends on the modules and integrations that are enabled.*

## 🧰 Technology Stack

### Primary Language

**Python**

Used for analysis logic, module integration, data processing, and automation of security checks.

### Graphical Interface

**PySide6 / Qt**

Used to build the desktop interface, organize application screens, and provide interactive features.

### Libraries and Components

| Technology | Purpose |
|---|---|
| `PySide6` | Desktop graphical user interface. |
| `pytest` | Automated testing. |
| `watchdog` | File and directory event monitoring, if used by active modules. |
| `Pillow` (`PIL`) | Image processing, where needed. |
| `OpenCV` (`cv2`) | Image processing and analysis, where needed. |
| `TensorFlow` | Machine learning capabilities, if integrated into the analysis workflow. |
| `PyTorch` | Machine learning capabilities, if integrated into the analysis workflow. |
| `PyPDF2` | PDF reading and manipulation, if used. |
| `python-dotenv` | Environment variable loading, if used for configuration. |

**Important:** This table distinguishes project-associated libraries from technologies whose actual use depends on the current codebase. Check `requirements.txt` and the corresponding modules to verify which dependencies are declared and actively used.

### Formats and Protocols

- **DNS:** Retrieve information associated with domain names.
- **RDAP:** Access domain registration and Internet resource registration data.
- **TLS:** Evaluate information related to encrypted connections.
- **JSON:** Represent analysis results and reports in a structured format.

## 🏗️ Project Architecture

PHISHGUARD follows a modular structure that separates the graphical interface from analysis and supporting components.

```text
phishguard/
├── app/
│   ├── analyzer.py
│   ├── ai_explainer.py
│   ├── correlation.py
│   ├── dns_lookup.py
│   ├── models.py
│   ├── rdap.py
│   ├── reputation.py
│   ├── routes.py
│   ├── storage.py
│   └── tls_check.py
├── tests/
├── desktop.py
├── run.py
├── requirements.txt
├── pytest.ini
├── .env.example
├── .gitignore
└── README.md
```

### Core Modules

- `desktop.py` — Entry point for the graphical desktop application.
- `analyzer.py` — Core URL analysis logic.
- `correlation.py` — Indicator organization and correlation.
- `dns_lookup.py` — DNS lookup functionality.
- `rdap.py` — RDAP query functionality.
- `reputation.py` — Reputation analysis module.
- `tls_check.py` — TLS-related checks.
- `ai_explainer.py` — Result explanation capabilities.
- `models.py` — Data structures used by the application.
- `routes.py` — Supporting functions and routing between components, according to the implementation.
- `storage.py` — Data persistence and retrieval.
- `tests/` — Automated tests.
- `requirements.txt` — Declared Python dependencies.
- `.env.example` — Example environment variable configuration, where applicable.

## 🖥️ Operating Systems

Development takes place in a Linux environment, with the goal of supporting distribution across multiple operating systems.

| Platform | Goal |
|---|---|
| Kali Linux | Development and testing in a cybersecurity environment. |
| Other Linux distributions | Compatibility to be validated through testing. |
| Windows | Future distribution as a standalone executable. |

Final compatibility depends on the application's dependencies and testing on each platform.

## 🧪 Testing and Quality

The project includes a structure for automated tests using `pytest`.

To run the tests in a configured development environment:

```bash
pytest -v
```

The `-v` option displays individual test results, making it easier to identify failures.

## 📥 Download

**The goal is to provide ready-to-use builds through the GitHub Releases page.**

<p align="center">
  <a href="https://github.com/john-root-opsec/phishguard/releases/latest">
    <img src="https://img.shields.io/badge/Download-PHISHGUARD-DC2626?style=for-the-badge&logo=github&logoColor=white" alt="Download PHISHGUARD">
  </a>
  <a href="https://github.com/john-root-opsec/phishguard">
    <img src="https://img.shields.io/badge/View-Source%20Code-27272A?style=for-the-badge&logo=github&logoColor=white" alt="Source code">
  </a>
</p>

**Note:** The download button currently links to the GitHub Releases page. Installers and executable files will become available once a packaged version has been published.

## 🗺️ Roadmap

- [x] Initial Python application structure.
- [x] PySide6 desktop interface.
- [x] Modular organization of analysis features.
- [x] Automated testing structure.
- [ ] Improve indicator correlation and interpretation.
- [ ] Validate all external integrations.
- [ ] Expand automated test coverage.
- [ ] Package the application for distribution.
- [ ] Publish a Windows executable.
- [ ] Publish an executable package for Linux.
- [ ] Automate release builds using GitHub Actions.

*The roadmap describes development goals and does not imply that all features are already complete.*

## 🔒 Security and Limitations

PHISHGUARD is a tool intended to support URL investigations. Its results should be treated as indicators rather than absolute guarantees of safety or malicious activity.

- A URL classified as suspicious requires contextual assessment.
- The absence of detected indicators does not guarantee that a URL is safe.
- External queries may share information about investigated domains with third-party services.
- Reputation and registration results depend on available data sources and service availability.
- Users should evaluate results before making security-related decisions.

Do not use this project to access, test, or exploit systems without authorization.

## 🎓 Educational and Professional Goals

PHISHGUARD is part of my software development and cybersecurity portfolio, demonstrating the practical application of skills in:

- Python application development.
- Modular programming and code organization.
- Desktop interfaces with PySide6.
- URL analysis and phishing indicators.
- Integration with network services and protocols.
- Automated testing.
- Data processing and persistence.
- Desktop application distribution.

The project demonstrates how programming knowledge can be applied to the development of tools for defensive security.

## 👨‍💻 Author

**John Root Opsec**

GitHub: [@john-root-opsec](https://github.com/john-root-opsec)

Repository: [PHISHGUARD](https://github.com/john-root-opsec/phishguard)

---

<p align="center">
  <sub>PHISHGUARD — Investigate indicators. Understand threats. Strengthen defense.</sub>
</p>
