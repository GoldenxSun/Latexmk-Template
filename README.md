# LaTeX Template

This repository provides a LaTeX template for creating your PDF documents. Below are the installation instructions, setup details, and a short explanation of the tools involved to get everything up and running smoothly.

## Tools Used

To work with this LaTeX template, you will need the following tools:

1. **MiKTeX**: A LaTeX distribution used to compile `.tex` files into PDF documents.
2. **Strawberry Perl**: A Perl programming language distribution for Windows, required by MiKTeX to automate certain processes like building LaTeX documents.
3. **Visual Studio Code (VSCode)**: A code editor that supports LaTeX editing with the help of extensions. We will use the **LaTeX Workshop** extension for compiling LaTeX directly within VSCode.

## Installation Instructions

### 1. Install MiKTeX

Download and install MiKTeX from the following link:

[MiKTeX Download](https://miktex.org/download)

- During the installation, allow the setup to automatically install missing LaTeX packages as needed.
- After installation, make sure to **update** MiKTeX via the console or settings panel to have the latest LaTeX packages.

### 2. Install Strawberry Perl

Download and install the following version or the **latest stable** version of Strawberry Perl:

[Strawberry Perl 5.32.1.1 (64-bit) Download](https://strawberryperl.com/download/5.32.1.1/strawberry-perl-5.32.1.1-64bit.zip)

- Extract the contents of the `.zip` file to the directory `C:\Users\user`.
- Run the following batch scripts to set it up:
  - `relocation.pl.bat`
  - `update_env.pl.bat`
- **Log out and log back in** to reload your environmental variables, ensuring your system recognizes Perl.

> **Note**: MiKTeX relies on Strawberry Perl for certain automated LaTeX commands, like using `latexmk` to compile your documents. This makes the entire process smoother.

### 3. Install Visual Studio Code (VSCode)

Download and install [Visual Studio Code](https://code.visualstudio.com/Download).

Once VSCode is installed, follow these steps to set it up for LaTeX:

1. Install the **LaTeX Workshop** extension:
   - Open the VSCode Marketplace and search for [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop).
   - Install the extension to allow LaTeX compiling and previewing within VSCode.

2. Open **User Settings**:
   - You can open it by pressing `Ctrl + Shift + P`, then searching for "Preferences: Open Settings".
   
3. Configure the **output directory**:
   - In the settings UI, set `Latex-workshop -> Latex: Out Dir` to `%DIR%/build`. This ensures that the compiled files (PDFs) go into a `build` folder within your project directory.

4. (optional) Open **User Settings (JSON)** and add the following configuration for LaTeX tools:
   - Press `Ctrl + Shift + P` again, search for "Preferences: Open Settings (JSON)", and add the following argument to LaTeX tools in the JSON settings under `args`:
   - Add `"-shell-escape"` for `latexmk`.

```json
{
    ...
    "latex-workshop.latex.outDir": "%DIR%/build",
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-shell-escape",
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        ...
    ],
    ...
}
```

### Why the `"-shell-escape"` option?

The `"-shell-escape"` flag is important for LaTeX because it allows the use of external programs in your LaTeX document, such as running scripts to generate plots or diagrams. Without this option, certain LaTeX packages that depend on shell commands won't work. This is especially helpful when you are working with more complex LaTeX documents that require automation or custom scripts.

## Cloning the Repository and Testing the Build

Once you have set up your environment, you can test if everything is working correctly by cloning this repository and compiling a test project:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/GoldenxSun/Latexmk-Template.git
   ```

2. **Navigate to the `Test` folder**:
   ```bash
   cd Latexmk-Template/Test
   ```

3. **Open the folder in Visual Studio Code**:
   ```bash
   code .
   ```

4. **Build the project**:
   - With the LaTeX Workshop extension installed, open the `main.tex` file in the `Test` folder.
   - Press `Ctrl + Alt + B` (or use the command palette `Ctrl + Shift + P` and run `LaTeX Workshop: Build LaTeX project`) to compile the LaTeX file.

If everything is set up correctly, the project should compile and produce a PDF `main.pdf` in the `build` folder. This will confirm that your LaTeX environment is working properly!
