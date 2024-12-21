# TypsTeX

TypsTeX is a LaTeX package
that allows you to **embed [Typst][typst] code in [LaTeX][latex] documents**.
Typst code wrapped in the `typst` environment
is dynamically compiled
and the resulting output is seamlessly integrated
as PDF images in your LaTeX document.

## Why?

[LaTeX][latex] is a powerful typesetting system,
but also notoriously difficult to work with,
especially for complex layouts and graphics.
[Typst][typst] is a much easier to use markup-based typesetting system
for the sciences.
It has powerful language features
for creating beautiful [documents][example_docs],
figures [[1][example_figs1], [2][example_figs2]],
and [plots][example_plots].
Unfortunately,
most, if not all, publishers are reluctant to accept Typst files,
and conferences do not offer official Typst templates.
This package bridges the gap between LaTeX and Typst,
by allowing you to embed Typst code in LaTeX documents.
You can now typeset your beautiful Typst figures and tables
in your LaTeX documents directly.

## Features

- Embed Typst code blocks directly within LaTeX.
- Dynamically compile Typst code into PDF using the Typst CLI.
- Supports passing custom flags to the Typst compiler.
- Automatically manages compilation based on content changes using MD5 checksums.

## Requirements

- LaTeX: A working LaTeX distribution.
- Typst: Ensure the Typst CLI is installed,
  and accessible via `typst` in the command line.
- POSIX-compliant shell: `echo`, `cat`, `md5sum`, `cmp`, `rm`, `mv`, `mkdir`.

## Usage

### Including the Package

Add the `typst.sty` file to your LaTeX working directory
and include it in your document:
```latex
\usepackage{typst}
```

### Typst Code Snippet

Wrap your Typst code in the typst environment. Example:
```latex
\begin{typst}{scale=1}
    #set text(size: 12pt)
    Hello, Typst in LaTeX!
\end{typst}
```
You can replace `scale=1` with any other `\includegraphics` options.

### Customize the Typst Preamble

You can define a custom preamble for Typst using the filecontents* environment:
```latex
\begin{filecontents*}[overwrite]{typst_premble.typ}
    #set page(width: auto, height: auto, margin: 0.5em)
    // Your extra Typst preamble here...
\end{filecontents*}
```

### Passing Flags to Typst Compiler

Customize the Typst compiler flags by redefining the `\typstflags` command:
```latex
\renewcommand{\typstflags}{--input ... --font-path ...}
```

### Compiling the Document

  1. Run `pdflatex --shell-escape example.tex`.
     It requires `--shell-escape` enabled in LaTeX for external command execution.
  2. The output PDF will embed the rendered Typst content.

### Structure

- `typst.sty`:
  This is the LaTeX package file that defines the typst environment.
  It handles:
  - Creating and managing Typst source files.
  - Compiling Typst code to PDFs via the typst CLI.
  - Detecting content changes to avoid redundant compilations.
  - Embedding the generated PDFs in LaTeX documents.

- `example.tex`:
  An example LaTeX document that demonstrates the use of the typst package.
  It includes:
  - How to set up Typst preambles.
  - Examples of embedding Typst code snippets.
  - Passing custom flags to the Typst compiler.

## Contributing

Feel free to submit issues or pull requests to improve this package.

Bugs:
- [ ] `typst compile` log files are not written for unknown reasons.

Features that may be added in the future:
- [ ] Include typst files by path.
- [ ] Unit tests.
- [ ] Better error handling and logging.
- [ ] A gallery of examples and use cases.
- [ ] CI workflow for automated testing and gallery compilation.
- [ ] Custom figure names for Typst output.
- [ ] Inline LaTeX commands in Typst code (I don't know if this is possible).

[typst]: https://typst.app/docs/
[latex]: https://www.latex-project.org/
[example_docs]: https://typst.app/universe/search/?kind=templates
[example_figs1]: https://github.com/cetz-package/cetz
[example_figs2]: https://github.com/Jollywatt/typst-fletcher
[example_plots]: https://github.com/cetz-package/cetz-plot
