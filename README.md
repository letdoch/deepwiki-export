# deepwiki-export

`deepwiki-export` is a command-line tool for downloading content from DeepWiki or GitHub URLs and processing it into multiple Markdown files organized by chapters. GitHub URLs are automatically converted to their corresponding DeepWiki URLs.

## Features

- Extract main content from DeepWiki/GitHub pages.
- Save each extracted content block (chapter) as a separate Markdown file.
- Output files are saved in a subdirectory automatically named based on the URL, located under the user-specified base output directory.
- For GitHub URLs, the subdirectory structure is `username/reponame/`.
- Support for preserving the original downloaded HTML file (saved in the same subdirectory).
- Configurable request and file encoding.

## Installation

Install from PyPI via pip (when released):
```bash
pip install deepwiki-export
```

Or install locally from source code (for development):
```bash
pip install -e .
```

## Usage

```
python -m deepwiki_export.cli_tool [OPTIONS] URL
```
Or, if installed via pip and added to PATH:
```bash
deepwiki-export [OPTIONS] URL
```

### Arguments

-   `URL`: (Required) The GitHub or DeepWiki URL to process.

### Options

| Option                        | Shorthand | Description                                                                                                                                | Default       |
| ----------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------- |
| `--output-base-dir DIR`       | `-o`      | Base output directory. A new subdirectory `user_name/repo_name` will be created under this directory to store output files.             | `.` (current directory) |
| `--keep-html`                 |           | Save the original downloaded HTML file (will be saved in the auto-generated output subdirectory).                                        | `False`       |
| `--html-encoding ENCODING`    |           | Encoding of the downloaded HTML content.                                                                                                  | `utf-8`       |
| `--md-encoding ENCODING`      |           | Encoding for the output Markdown files. If not set, defaults to HTML encoding.                                                           | `None`        |
| `--user-agent STRING`         |           | Custom User-Agent string for HTTP requests. Overrides the default.                                                                        | `None`        |
| `--timeout SECONDS`           |           | HTTP request timeout in seconds.                                                                                                          | `30`          |
| `--version`                   |           | Show application version and exit.                                                                                                        |               |
| `--verbose`                   | `-v`      | Enable verbose output (DEBUG level logging).                                                                                              | `False`       |
| `--help`                      | `-h`      | Show help information and exit.                                                                                                           |               |

## Example

Suppose you want to export content from a DeepWiki page of the Roo Code project and want the output to go to a `my_exports` base directory under the current directory:

```bash
deepwiki-export --output-base-dir ./my_exports "https://deepwiki.com/RooVetGit/Roo-Code/some-page" --keep-html
```

This will:
- Download content from the specified DeepWiki URL.
- Create a subdirectory named `RooVetGit_Roo-Code` (or similar, depending on the specific implementation of `derive_dirname_from_url`) under the `./my_exports/` directory.
- Inside that subdirectory (`./my_exports/RooVetGit_Roo-Code/`), save each extracted chapter as a separate Markdown file (e.g., `chapter_1.md`, `chapter_2.md`, ...).
- Additionally, the original HTML file (e.g., `_original_page.html`) will also be saved in this subdirectory.

## Contributing

Issues, bug reports, and feature requests are welcome.

## License

This project is licensed under the [MIT License](LICENSE).