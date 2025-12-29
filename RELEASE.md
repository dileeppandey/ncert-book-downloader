# Release Guide

This guide describes how to publish `ncert-book-downloader` to PyPI and how to run it using `pipx`.

## Prerequisites

1.  A [PyPI account](https://pypi.org/account/register/).
2.  An [API token](https://pypi.org/help/#apitoken) for PyPI.
3.  The `build` and `twine` packages installed:
    ```bash
    pip install build twine
    ```

## Publishing to PyPI

### 1. Build the distribution files

Run the following command in the project root:
```bash
python3 -m build
```
This will create a `dist/` directory with `.tar.gz` and `.whl` files.

### 2. Upload to PyPI

Use `twine` to upload the distributions:
```bash
python3 -m twine upload dist/*
```
When prompted, use `__token__` as the username and your API token as the password.

> [!TIP]
> You can also use a `.pypirc` file to automate the authentication.

---

## Running with pipx

`pipx` is the recommended way to run this tool as a standalone CLI application without polluting your global Python environment.

### 1. Install pipx

If you don't have `pipx` installed:
```bash
brew install pipx
pipx ensurepath
```

### 2. Install the tool

Once the package is on PyPI:
```bash
pipx install ncert-book-downloader
```

### 3. Run the tool

You can now run the tool from anywhere:
```bash
ncert-download --list
```

### 4. Direct execution without installation

You can also run it temporarily without installing:
```bash
pipx run ncert-book-downloader --classes 10
```

---

## Testing locally

To test the installation locally before publishing:

### Using pipx
```bash
pipx install . --force
```

### Using pip
```bash
pip install .
```
