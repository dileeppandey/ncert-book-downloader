# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-28

### Added
- Initial public release
- Download all NCERT textbooks (Classes 1-12) in PDF format
- Support for both English and Hindi medium books
- Parallel downloads with configurable workers
- Resume support - automatically skip already downloaded files
- Automatic ZIP extraction to get PDF files
- PDF chapter merging into single book files
- Flexible filtering by class, subject, or language
- Beautiful CLI with progress indicators and colored output
- Comprehensive book organization utilities
- MIT License for open source distribution

### Supported Subjects
- **Classes 11-12**: Physics, Chemistry, Maths, Biology, Accountancy, Business Studies, Economics, Geography, History, Political Science, Psychology, Sociology, Hindi, English
- **Classes 9-10**: Science, Maths, Social Science, Hindi, English
- **Classes 6-8**: Science, Maths, Social Science, Hindi, English
- **Classes 3-5**: Maths, EVS (Environmental Studies), Hindi, English
- **Classes 1-2**: Maths, Hindi, English

### Technical Details
- Built with Python 3.9+ compatibility
- Uses `requests` for HTTP operations
- Optional `pypdf` integration for PDF merging
- Modern `pyproject.toml` based packaging
- Comprehensive type hints and documentation

## [Unreleased]

### Planned
- Web interface for book selection
- Progress bar for large downloads
- Automatic retry with better error handling
- Book metadata extraction

---

[1.0.0]: https://github.com/dpandey/ncert-book-downloader/releases/tag/v1.0.0
[Unreleased]: https://github.com/dpandey/ncert-book-downloader/compare/v1.0.0...HEAD
