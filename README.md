# Switching_Between_Movement_Patterns

**Mathematical Modeling — IEAP Final Project, Group E**  
**Université de Montpellier**

**Group members:** Gaia Gassiole, Chloé Gilles, and Jennifer Houmard

## 1. Project Overview

This project investigates how an external instruction can change an athlete's preference between two movement patterns, called **Pattern A** and **Pattern B**.

The main research question is:

**How does an external instruction favouring Pattern B affect the stability of coordination preferences, and can it cause a switch from Pattern A to Pattern B?**

We use a simple mathematical model to study how coordination preferences change over time. We first analyse the model without an instruction, then introduce a positive instruction favouring Pattern B.

As an additional analysis, we also test a weaker positive instruction to investigate whether the strength of the instruction matters.

The two patterns are abstract and do not represent specific movements or measurements from real athletes.

## 2. Mathematical Model

The model is described by the differential equation:

$$
\dot{x} = 1.2x - 0.8x^3 + I
$$

Where:

- **$x$:** Coordination preference. Negative values favour Pattern A, positive values favour Pattern B, and zero represents no preference.
- **$\dot{x}$:** Rate of change of the coordination preference.
- **$I$:** External instruction. Positive values favour Pattern B, while negative values favour Pattern A.

The values 1.2 and 0.8 remain constant. The instruction $I$ is also constant during each simulation but can change between conditions.

An **equilibrium** is a value of $x$ where $\dot{x}=0$ and the preference does not change.

- A **stable equilibrium** attracts nearby preferences.
- An **unstable equilibrium** pushes nearby preferences away.

## 3. Method and Main Findings

### Method

We use Python to:

1. Calculate the equilibria of the model.
2. Determine their stability using the sign of $\dot{x}$.
3. Use the explicit Euler method to simulate how the preference changes over time.
4. Compare the results under different instruction conditions.

The Euler simulations use the following settings:

| Parameter | Value |
|---|---|
| Time step | $h=0.01$ |
| Simulation time | $t=0$ to $t=20$ |
| Initial preferences | $x(0)=-1.8$ and $x(0)=+1.8$ |
| Number of steps | 2000 |

### Main Findings

| Instruction | Stable equilibria | Main result |
|---|---|---|
| $I=0$ | $x\approx-1.225$ and $x\approx+1.225$ | Both patterns are stable. Each starting preference approaches the stable equilibrium on its own side. |
| $I=0.70$ | $x\approx+1.450$ | Only the Pattern B equilibrium remains. Both starting preferences approach Pattern B. |
| $I=0.40$ | $x=-1.000$ and $x\approx+1.366$ | Pattern A is still stable. A preference starting at $-1.8$ would remain on the Pattern A side. |

For $I=0$, the model has two stable equilibria separated by an unstable equilibrium at $x=0$.

For $I=0.70$, the negative stable equilibrium and the unstable equilibrium disappear. The preference starting at $-1.8$ crosses zero and approaches the remaining stable equilibrium favouring Pattern B.

The $I=0.40$ condition was an additional analysis beyond the assignment requirements. It shows that a positive instruction does not necessarily cause a switch.

**Main conclusion:** Both the direction and the strength of an instruction matter. A sufficiently strong positive instruction can cause a preference to switch towards Pattern B, but a weaker instruction may not.

**Model limitation:** The model is deterministic and does not include natural variability or unexpected disturbances in an athlete's coordination. It helps explain possible changes in a simplified system but cannot predict exactly how a real athlete would respond.

## 4. Project Structure

The project is organised as follows:

```text id="k8i7jr"
Switching_Between_Movement_Patterns/
│
├── master.qmd                         # Main Quarto report
├── README.md                          # Project documentation
├── references.bib                     # Bibliography
├── .gitignore
├── LICENSE
│
├── sections/
│   ├── 01_introduction.qmd
│   ├── 02_understanding_the_model.qmd
│   ├── 03_equilibria_and_stability.qmd
│   ├── 04_euler_simulations.qmd
│   ├── 05_effect_of_parameters.qmd
│   └── 06_appendix.qmd
│
├── figures/
│   └── model_comparison.png           # Instruction comparison diagram
│
└── styles/
    └── apa.csl                        # APA citation style
```

The `master.qmd` file contains the YAML configuration, shared Python imports, and table of contents. It combines the five main sections, references, and appendices into one report.

Sections 03, 04, and 05 share Python functions and variables, so they must be executed in order.

The appendices contain the Python code for Sections 03–05 and the group workflow.

## 5. Why We Used Quarto and VS Code

We chose Quarto with VS Code because it is designed to create structured reports that combine written explanations, mathematical equations, Python code, and figures.

The main advantage of Quarto for our project was its document organisation. We could divide the report into separate .qmd files and combine them automatically using master.qmd. This allowed each group member to work independently while contributing to the same report.

Quarto was also well suited to GitHub collaboration. Since .qmd files are plain text, we could easily track changes, review pull requests, leave comments, and resolve conflicts between different versions.

Another benefit was its centralised report configuration. We could manage the PDF layout, figure numbering, cross-references, bibliography, and code visibility from one main file. This helped maintain consistent formatting across all sections.

Finally, Quarto allowed us to automatically generate the complete report. Rendering master.qmd executes the Python calculations in order, updates the figures, and produces the final PDF without manually combining the sections.

We used VS Code to develop and organise the files, while Jupyter executed the Python code through Quarto.

Overall, Quarto provided a clear and efficient workflow for collaborative writing, version control, and automatic report generation.


## 6. How to Run the Project

### Requirements

- [Quarto](https://quarto.org/)
- Python 3 with NumPy, Matplotlib, and Jupyter
- A LaTeX distribution for PDF rendering (e.g., TinyTeX)

VS Code is recommended for editing the `.qmd` files but is not required to render the report.

### Installation and Rendering

**1. Install Quarto**

Download and install Quarto for your operating system from the [official Quarto website](https://quarto.org/docs/get-started/).

After installation, verify that Quarto is available:

```bash
quarto --version
```

**2. Clone the GitHub repository**

```bash
git clone https://github.com/jenniferhoumard/Switching_Between_Movement_Patterns.git
cd Switching_Between_Movement_Patterns
```

**3. Install TinyTeX (if no LaTeX distribution is installed)**

```bash
quarto install tinytex
```

**4. Render the complete PDF report**

```bash
quarto render master.qmd --to pdf
```

The generated PDF is saved as `master.pdf`.

The `master.qmd` file executes the Python code in the correct order and generates the figures automatically. The appendices display the corresponding Python code without executing it again.

**Note:** The report uses the `python3` Jupyter kernel specified in `master.qmd`. This kernel must have access to NumPy and Matplotlib.

## 7. Group Organisation

The project was divided between three group members. Each member was responsible for specific Quarto sections.

| Group member | Assigned Quarto documents |
|---|---|
| Jennifer Houmard (GitHub setup) | 01 Introduction, 05 Effect of Parameters |
| Gaia Gassiole | 02 Understanding the Model, 04 Euler Simulations |
| Chloé Gilles | 03 Equilibria and Stability, 06 Appendix |

One member created the GitHub repository and prepared the initial Quarto project structure. Each section contained predefined headings and short guidelines explaining what needed to be included.

This allowed members to work independently while following the same organisation.

All members participated in reviewing the sections, checking the mathematical results, improving explanations, and validating the final report.

## 8. Git Branching Strategy

A separate GitHub branch was created for each Quarto section.

| Branch | Assigned member |
|---|---|
| `01_introduction` | Jennifer Houmard |
| `02_understanding_the_model` | Gaia Gassiole |
| `03_equilibria_and_stability` | Chloé Gilles |
| `04_euler_simulations` | Gaia Gassiole |
| `05_effect_of_parameters` | Jennifer Houmard |
| `06_Appendix` | Chloé Gilles |

### Workflow

1. Create a branch from the latest `main` branch.
2. Develop the assigned `.qmd` section using the predefined headings and guidelines.
3. Commit and push changes to the corresponding branch.
4. Open a pull request into `main`.
5. The other group members review the changes and leave comments suggesting corrections or improvements.
6. Update the branch to address the feedback.
7. Merge the reviewed and approved pull request into `main`.
8. Render the complete report and verify the mathematical results, figures, references, and formatting.

Direct changes to `main` are avoided during development. Pull requests allow us to review each other's contributions before integrating them into the main report.

This workflow helped us divide responsibilities, track changes, and maintain consistency between the different sections.

## 9. License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

See the [LICENSE](LICENSE) file for details.

