# Contributing to NCERT Book Downloader

Thank you for your interest in contributing to NCERT Book Downloader! This document provides guidelines and instructions for contributing.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Fixing Broken Links](#fixing-broken-links)
- [Adding New Languages](#adding-new-languages)
- [Adding New Books](#adding-new-books)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Release Procedures](#release-procedures)

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

---

## 🔗 Fixing Broken Links

NCERT occasionally updates their website structure, which can break download links. If you find a broken link:

### Step 1: Find the Correct URL

1. Visit the [NCERT Textbooks Page](https://ncert.nic.in/textbook.php)
2. Navigate to the class and subject
3. Look for the "Download Complete Book" ZIP option
4. Right-click and copy the link address

### Step 2: Verify the URL Works

```bash
# Check if the URL is accessible (should return 200 OK)
curl -I "https://ncert.nic.in/textbook/pdf/YOUR_NEW_URL.zip"

# Or download and verify the file
wget "https://ncert.nic.in/textbook/pdf/YOUR_NEW_URL.zip"
```

### Step 3: Update the Book Entry

1. Open `ncert_downloader/books.py`
2. Find the book with the broken link
3. Update the `url` field with the correct URL
4. Submit a Pull Request with your fix

**Example fix:**
```python
# Before (broken)
Book(10, "Science", "Science", "English", "https://ncert.nic.in/textbook/pdf/OLD_URL.zip"),

# After (fixed)
Book(10, "Science", "Science", "English", "https://ncert.nic.in/textbook/pdf/jesc1dd.zip"),
```

### Quick Fix via Issue

If you're not comfortable with code, simply [open an issue](https://github.com/dpandey/ncert-book-downloader/issues/new) with:
- The book that failed to download
- The error message you received
- The correct URL (if you found it)

---

## 🌐 Adding New Languages

NCERT provides textbooks in regional languages like Urdu, Assamese, Bengali, Gujarati, Kannada, Malayalam, Marathi, Odia, Punjabi, Tamil, and Telugu. We welcome contributions to add these!

### Step 1: Find Regional Language Books

1. Visit [NCERT Textbooks](https://ncert.nic.in/textbook.php)
2. Select your target language from the dropdown
3. Browse available books and collect their download URLs

### Step 2: Update the Models (if needed)

If adding a new language, verify it works with the existing `Book` model. The `language` field accepts any string:

```python
# Example: Adding Urdu books
Book(10, "Science", "سائنس", "Urdu", "https://ncert.nic.in/textbook/pdf/jusc1dd.zip"),
```

### Step 3: Add Books to the Catalog

1. Open `ncert_downloader/books.py`
2. Add a new section for your language:

```python
# ==================== CLASS 10 (URDU) ====================
Book(10, "Science", "سائنس", "Urdu", "https://ncert.nic.in/textbook/pdf/jusc1dd.zip"),
Book(10, "Maths", "ریاضی", "Urdu", "https://ncert.nic.in/textbook/pdf/jumh1dd.zip"),
# ... add more books
```

### Step 4: Update CLI Language Choices

Open `ncert_downloader/cli.py` and add the new language to the choices:

```python
parser.add_argument(
    "-l", "--language",
    nargs="+",
    choices=["English", "Hindi", "Urdu", "english", "hindi", "urdu"],  # Add new language
    ...
)
```

### Step 5: Update Documentation

- Add the new language to `README.md` in the features section
- Update `CHANGELOG.md` to note the addition

### Regional Language URL Patterns

NCERT uses a predictable URL pattern. The first letter typically indicates the language:
- `e` = English (e.g., `jesc1dd.zip`)
- `h` = Hindi (e.g., `jhsc1dd.zip`)
- `u` = Urdu (e.g., `jusc1dd.zip`)
- Other languages follow similar patterns

---

## 📚 Adding New Books

To add new books that are missing from the catalog:

1. Open `ncert_downloader/books.py`
2. Add a new `Book` entry with the correct metadata:
   ```python
   Book(
       class_num=10,           # Class number (1-12)
       subject="Science",       # Subject name (use underscores for multi-word: "Social_Science")
       title="Book Title",      # Book title (can be in any language)
       language="English",      # Language of the book
       url="https://...",       # Direct ZIP download URL
       part=1                   # Optional: Part number for multi-part books
   )
   ```

3. Place the book in the correct section (organized by class)
4. Verify the URL is accessible:
   ```bash
   curl -I "https://ncert.nic.in/textbook/pdf/example.zip"
   ```

5. Test the download works:
   ```bash
   python -m ncert_downloader.cli --classes 10 --subjects Science --language English
   ```

---

## Pull Request Process

1. Create a new branch for your changes:
   ```bash
   git checkout -b fix/broken-class10-science-link
   # or
   git checkout -b feature/add-urdu-support
   ```

2. Make your changes and commit with clear messages:
   ```bash
   git commit -m "Fix: Update Class 10 Science English download URL"
   # or
   git commit -m "Add: Urdu language support with Class 10 books"
   ```

3. Ensure your code passes linting and tests:
   ```bash
   ruff check .
   pytest
   ```

4. Push to your fork and create a Pull Request

5. In your PR description, include:
   - What you changed and why
   - How you verified the links work
   - Any testing you performed

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

## Release Procedures

If you have permission to release new versions of the package:

1.  **Update Version**: Increment the version in `pyproject.toml`.
2.  **Update Changelog**: Add the new version and its changes to `CHANGELOG.md`.
3.  **Build**: Run `python3 -m build` to generate distribution files.
4.  **Publish**: Upload to PyPI using `twine upload dist/*`.

See [RELEASE.md](RELEASE.md) for more detailed instructions and PyPI authentication tips.

## Running with pipx

For development and testing of the CLI, it's recommended to use `pipx`:

```bash
pipx install . --force
```

This installs the package in a isolated environment while making the `ncert-download` command available globally in your terminal.

## Questions?

Feel free to open an issue if you have questions or need help getting started!

---

Thank you for contributing! 🙏
