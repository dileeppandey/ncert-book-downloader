# Contributing to NCERT Book Downloader

Thank you for your interest in contributing to NCERT Book Downloader! This document provides guidelines and instructions for contributing.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Reporting Bugs](#reporting-bugs)
- [Requesting Features](#requesting-features)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Adding New Books](#adding-new-books)

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment for everyone.

## Getting Started

1. Fork the repository on GitHub
2. Clone your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/ncert-book-downloader.git
   cd ncert-book-downloader
   ```

## Development Setup

1. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install the package in development mode with dev dependencies:
   ```bash
   pip install -e ".[dev,merge]"
   ```

3. Run the tests to verify your setup:
   ```bash
   pytest
   ```

## How to Contribute

### Reporting Bugs

Before creating a bug report:
- Check if the issue already exists in the [Issues](https://github.com/dpandey/ncert-book-downloader/issues) section
- Include as much detail as possible:
  - Python version (`python --version`)
  - Operating system
  - Complete error messages
  - Steps to reproduce the issue

### Requesting Features

Feature requests are welcome! Please:
- Check if the feature is already requested
- Clearly describe the use case
- Explain how the feature would benefit users

### Pull Request Process

1. Create a new branch for your changes:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes and commit with clear messages:
   ```bash
   git commit -m "Add: description of your changes"
   ```

3. Ensure your code passes linting and tests:
   ```bash
   ruff check .
   pytest
   ```

4. Push to your fork and create a Pull Request

5. Wait for review and address any feedback

## Coding Standards

- Follow PEP 8 style guidelines
- Use type hints for function signatures
- Write docstrings for public functions and classes
- Keep functions focused and modular
- Add comments for complex logic

### Code Formatting

We use `ruff` for linting. Before committing:

```bash
ruff check .
ruff format .
```

## Adding New Books

To add new books or fix broken links:

1. Open `ncert_downloader/books.py`
2. Add a new `Book` entry with the correct metadata:
   ```python
   Book(
       class_num=10,           # Class number (1-12)
       subject="Science",       # Subject name
       title="Book Title",      # Book title
       language="English",      # "English" or "Hindi"
       url="https://...",       # Direct download URL
       part=1                   # Optional: Part number
   )
   ```

3. Verify the URL is accessible:
   ```bash
   curl -I "https://ncert.nic.in/textbook/pdf/example.zip"
   ```

4. Test the download works

## Questions?

Feel free to open an issue if you have questions or need help getting started!

---

Thank you for contributing! 🙏
