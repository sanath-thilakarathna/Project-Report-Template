# Project Report Template (LaTeX)

This repository is a LaTeX report template with a structured `sections/`, `figures/`, and `tables/` layout.

## Prerequisites

Install a LaTeX distribution that includes `latexmk` and `biber`:

- **Windows (recommended):** MiKTeX (with on-the-fly package install enabled) or TeX Live
- Ensure these commands are available in your terminal: `latexmk`, `pdflatex`, `biber`

## Quick start (build the PDF)

From the repository root:

```powershell
latexmk -pdf main.tex
```

Output: `main.pdf`

### Clean build artifacts

```powershell
latexmk -c
```

(Use `latexmk -C` for a more aggressive clean.)

## Editing the content

The entry point is `main.tex`. It defines basic metadata (title, student name, etc.) and includes the content files.

### Update report metadata

Edit the simple macros near the top of `main.tex`, for example:

- `\ProjectTitle`
- `\StudentName`, `\StudentID`
- `\SupervisorName`
- `\SubmissionDate`

### Sections

Chapter/section content lives in `sections/` and is included from `main.tex` via `\input{...}`:

- `sections/titlepage.tex`
- `sections/introduction.tex`
- `sections/requirements.tex`
- `sections/design.tex`
- `sections/implementation.tex`
- `sections/testing.tex`
- `sections/results.tex`
- `sections/conclusion.tex`
- Appendices: `sections/appendix_a.tex`

### Figures

Place images (PDF/PNG/JPG) and/or LaTeX/TikZ figure files under `figures/`.

Example (including a LaTeX figure file):

```tex
\input{figures/block_diagram}
```

Example (including an image file):

```tex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.9\textwidth]{figures/your_figure.png}
  \caption{Your caption}
  \label{fig:your_label}
\end{figure}
```

### Tables

Reusable tables are under `tables/`.

Example:

```tex
\input{tables/acceptance_criteria}
```

## References / citations

This template uses `biblatex` with the **`biber`** backend:

- Bibliography database: `references.bib`
- Printed in `main.tex` via `\printbibliography`

Add new entries to `references.bib`, then cite them in your text:

```tex
As shown in \cite{sedra_smith_microelectronic_2014} ...
```

`latexmk -pdf main.tex` will run the required `biber` passes automatically.

## VS Code + LaTeX Workshop + MiKTeX (recommended on Windows)

1) Install **MiKTeX**

- Open *MiKTeX Console* and enable **Install missing packages on-the-fly**.
- Ensure these tools are installed/available on PATH (MiKTeX can install them as needed): `pdflatex`, `latexmk`, `biber`.

2) Install the VS Code extension **LaTeX Workshop**

- Extension ID: `James-Yu.latex-workshop`

3) Build and preview

- Open this repo folder in VS Code
- Open `main.tex`
- Run **“LaTeX Workshop: Build LaTeX project”**
- Run **“LaTeX Workshop: View LaTeX PDF file”**

4) (Optional) Recommended settings for `latexmk` + `biber`

Create or edit `.vscode/settings.json` (workspace settings) and add:

```json
{
  "latex-workshop.latex.recipe.default": "latexmk (pdf)",
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "%DOC%"
      ]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "latexmk (pdf)",
      "tools": ["latexmk"]
    }
  ]
}
```

This template uses `biblatex` with the `biber` backend, and `latexmk` will run `biber` automatically.

## Troubleshooting

- If compilation fails due to missing packages on MiKTeX, allow it to install packages when prompted.
- If references show as `??`, run a full build again: `latexmk -pdf main.tex`.
