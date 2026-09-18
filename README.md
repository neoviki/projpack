# projpack

Flatten an entire project (directory tree + file contents) into a single
portable file with **`pjexport`**, and reconstruct it later - exact
structure, exact content - with **`pjimport`**.

Useful for:

* Pasting a whole codebase into an LLM prompt (for small projects)
* Sending a project as a single attachment
* Snapshotting and restoring a project tree
* Comparing two project snapshots to quickly identify added, removed, or modified files

## Install

```bash
# Directly from Git (recommended)
pipx install git+https://github.com/neoviki/projpack.git

# From a cloned checkout
pip install .

# From a cloned checkout, isolated
pipx install .
```

All methods install the `pjexport` and `pjimport` commands on your `PATH` — no
manual `chmod` or symlinking needed.


```bash
pjexport --help
pjimport --help
```
## Update to a Newer Version

If installed with `pipx`, update the installed package with:

```bash
pipx upgrade projpack
```

To reinstall directly from the latest Git repository version:

```bash
pipx uninstall projpack
pipx install git+https://github.com/neoviki/projpack.git
```

## Uninstall

To remove `projpack`:

```bash
pipx uninstall projpack
```

This removes the installed `pjexport` and `pjimport` commands.


## Usage

### Export

```bash
pjexport .                          # export current dir -> project.export
pjexport . -o mybackup.txt          # any output name/extension works
pjexport . -e exclude.csv           # apply exclusions from a CSV
```

### Import (restore)

```bash
pjimport project.export                        # restore into current dir
pjimport project.export -d ./restored           # restore into another dir
pjimport project.export --overwrite              # overwrite existing files
pjimport project.export --dry-run                # preview only, no writes
```

## Exclude CSV Format

You can keep the files, directories, and extensions you want to exclude in
a CSV file, for example `exclude.csv`.

For example:

```text
src1
.txt
app/test.py
app/pycache
node_modules
.log
```

Each line can contain a file, directory, extension, or path to exclude.

- No `/` and a matching **directory** exists anywhere in the tree -> excludes that directory name everywhere
- Starts with `.` -> excluded as a file **extension**, everywhere
- No `/` and a matching **file** exists anywhere in the tree -> excludes that filename everywhere
- Contains `/` -> excluded as an **exact path** relative to the project root (file or directory)

## Notes

- All plain-text source files are included by default (Python, Rust, Go,
  C/C++, Java, LaTeX, HTML, etc.) - only binary/compiled artifacts
  (`.pyc`, `.dll`, `.jar`, images, ...) are excluded by default.
- The tree preview inside the export file always shows a generic
  `Project_Root/` label instead of your real folder name (override with
  `--root-label`).
- `pjexport` prints the resolved directory it's about to scan
  (`Scanning: /abs/path`) before it runs, so you can confirm it's using
  the folder you expect.

## License

MIT - see [LICENSE](LICENSE).

## Acknowledgments

This project was developed collaboratively with the support of LLM-based tools, including Claude Sonnet 5, Perplexity, and OpenAI. These tools supported the project’s optimization, documentation, installation instructions, and test-case preparation.
