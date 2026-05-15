# Getting Started with Python using Conda

A beginner's guide for installing Python and managing virtual environments — for students who have never used Python before.



## Table of Contents

1. [What Is This Guide About?](#what-is-this-guide-about)
2. [Key Terms (Read This First)](#key-terms-read-this-first)
3. [Step 1 — Installing Conda](#step-1--installing-conda)
   - [Windows](#windows-installation)
   - [Mac](#mac-installation)
4. [Step 2 — Checking Your Installation](#step-2--checking-your-installation)
5. [Step 3 — Working with Virtual Environments](#step-3--working-with-virtual-environments)
6. [Step 4 — Installing Packages](#step-4--installing-packages)
7. [Step 5 — Writing Code in VS Code](#step-5--writing-code-in-vs-code)
8. [Maintenance — Cleaning Cache & Freeing Up Space](#maintenance--cleaning-cache--freeing-up-space)
9. [Troubleshooting Common Problems](#troubleshooting-common-problems)
10. [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
11. [Quick Command Cheat Sheet](#quick-command-cheat-sheet)


## What Is This Guide About?

Python is a programming language. To *run* Python on your computer, you need to install it. We will use a tool called **Conda** to do this.

Why Conda instead of installing Python directly?

- It installs Python *and* helps you install extra tools (called "packages").
- It lets you create separate "workspaces" so different projects don't interfere with each other.
- It works almost the same way on Windows and Mac, so this guide covers both.

You will be typing commands into a **terminal** (a text-based window for giving your computer instructions). Don't worry — every command you need is written out for you. Just copy, paste, and press Enter.

---

## Key Terms (Read This First)

| Term | What it means |
|------|---------------|
| **Terminal / Command line** | A window where you type commands instead of clicking buttons. On Windows it's called *Anaconda Prompt*; on Mac it's called *Terminal*. |
| **Conda** | The program that installs and manages Python for you. |
| **Miniconda** | A small, lightweight version of Conda. This is what we will install. |
| **Package** | An add-on tool for Python (for example, `pandas` for working with data). |
| **Virtual environment** | A separate, isolated workspace for one project. Keeps each project's tools from clashing. |
| **`base` environment** | The default environment that exists right after installation. Best practice: don't install your project tools here. |
| **VS Code** | A free code editor where you'll actually write and run your Python code. |
| **Extension** | An add-on for VS Code that gives it new abilities (you'll install ones for Python and Jupyter). |
| **Interpreter / Kernel** | The specific Python that VS Code uses to run your code. You point this at your conda environment. |


## Step 1 — Installing Conda

We will install **Miniconda** — it's smaller and faster to install than the full Anaconda. It also builds a good habit: you install only the packages each project actually needs, instead of carrying around hundreds you'll never use.

### Windows Installation

1. Go to the official Miniconda download page: <https://www.anaconda.com/download/success>
2. Under **Miniconda Installers**, download the **Windows 64-bit** installer (a `.exe` file).
3. Double-click the downloaded `.exe` file to start the installer.
4. Click through the installer with these choices:
   - **Install for:** "Just Me" (recommended)
   - **Destination folder:** leave the default
   - **Advanced options:** leave the default boxes checked. (You do *not* need to add Conda to PATH — we'll use the Anaconda Prompt instead.)
5. Click **Install** and wait for it to finish, then click **Finish**.
6. Open the **Start Menu**, type `Anaconda Prompt`, and click it. A black terminal window will open.

> From now on, whenever this guide says "open your terminal," Windows users should open **Anaconda Prompt**.

### Mac Installation

There are two common Macs: ones with **Apple Silicon** (M1, M2, M3, M4 chips — most Macs from 2020 onward) and older ones with **Intel** chips.

**How to check which one you have:** Click the Apple logo (top-left) → *About This Mac* → look at the "Chip" or "Processor" line.

1. Go to the official Miniconda download page: <https://www.anaconda.com/download/success>
2. Under **Miniconda Installers**, download the macOS installer that matches your Mac:
   - Apple Silicon → **macOS Apple M1 64-bit pkg**
   - Intel → **macOS Intel x86 64-bit pkg**
3. Double-click the downloaded `.pkg` file and follow the installer steps (keep the defaults). Enter your Mac password if asked.
4. When it finishes, open the **Terminal** app:
   - Press `Cmd + Space`, type `Terminal`, press Enter.
5. Close the Terminal window and open a new one (this lets the changes take effect).

> From now on, whenever this guide says "open your terminal," Mac users should open the **Terminal** app.


## Step 2 — Checking Your Installation

Open your terminal and type this command, then press Enter:

```bash
conda --version
```

If you see something like `conda 24.x.x`, the installation worked. 🎉

Next, check that Python is available:

```bash
python --version
```

You should see something like `Python 3.12.x`.

You may notice your terminal line now starts with `(base)`. That's normal — it means you're currently in the default `base` environment.

---

## Step 3 — Working with Virtual Environments

A **virtual environment** is a separate workspace for one project. Think of it like a clean desk for each assignment: tools from one project won't mess up another.

You can always remove a virtual environment when you no longer need it, to free up storage space.

**Golden rule:** Create a new environment for each project. Never install project tools in `base`.

### Create a new environment

Let's create an environment named `myproject` with Python 3.12:

```bash
conda create --name myproject python=3.12
# Feel free to change the Python version to a newer one
```

When it asks `Proceed ([y]/n)?`, type `y` and press Enter.

> You can name the environment anything you like. Use a short, lowercase name with no spaces — for example `stats101` or `data-class`.

### Activate (enter) an environment

Before you work on a project or install a package into a specific environment, you must **activate** that environment:

```bash
conda activate myproject
```

Your terminal line (on the left) will change from `(base)` to `(myproject)`. This tells you which environment you are in.

### Deactivate (leave) an environment

When you're done, return to `base` with:

```bash
conda deactivate
```

### See all your environments

```bash
conda env list
```

The environment with a `*` next to it is the one you're currently in.

### Delete an environment you no longer need

```bash
conda remove --name myproject --all
```

This frees up disk space. Make sure you've run `conda deactivate` first if you're inside it.


## Step 4 — Installing Packages

Packages are add-on tools for an environment. **Always activate your environment first**, then install.

```bash
conda activate myproject
conda install numpy pandas matplotlib
```

This installs three popular packages for data work. Type `y` when prompted.

If a package isn't available through conda, you can use `pip` (Python's other package installer) — but only *inside an activated environment*:

```bash
pip install some-package-name
```

### See what's installed in the current environment

```bash
conda list
```


## Step 5 — Writing Code in VS Code

So far you've installed Python and created an environment. Now you need somewhere to actually *write* your code. We'll use **Visual Studio Code (VS Code)** — a free, beginner-friendly code editor that works on both Windows and Mac.

### Install VS Code

1. Go to <https://code.visualstudio.com> and click the big download button (it detects your operating system automatically).
2. **Windows:** run the downloaded installer, keep the default options, and check the box **"Add to PATH"** if it appears.
3. **Mac:** open the downloaded file, then drag the **Visual Studio Code** icon into your **Applications** folder.
4. Open VS Code once it's installed.

### Install the Python and Jupyter extensions

Extensions add features to VS Code. You need two.

1. In VS Code, click the **Extensions** icon in the left sidebar (it looks like four squares), or press `Ctrl+Shift+X` (Windows) / `Cmd+Shift+X` (Mac).
2. In the search box, type `Python` and install the one published by **Microsoft**.
3. Search for `Jupyter` and install that one (also by **Microsoft**). This lets you run notebooks.

You only need to do this once.

### Open your project folder

VS Code works best when you open a *folder*, not just a single file.

1. Create a folder somewhere for your project, for example `my-first-project`.
2. In VS Code: **File → Open Folder...** and select that folder.

### Select your conda environment (the most important step!)

This is the step beginners most often miss. VS Code needs to know **which Python to use** — and you want it to use the conda environment you created, not some other Python.

1. Open the Command Palette: press `Ctrl+Shift+P` (Windows) / `Cmd+Shift+P` (Mac).
2. Type `Python: Select Interpreter` and press Enter.
3. A list appears. Choose the one that mentions your environment name — it will look something like:
   `Python 3.12.x ('myproject': conda)`

> If you don't see your environment in the list, close VS Code completely and reopen it. If it's still missing, make sure you actually created the environment (Step 3).

Once selected, VS Code remembers this choice for the folder.

### Option A — Run a Python script (`.py` file)

1. In VS Code's file explorer (left sidebar), create a new file called `hello.py`.
2. Type this into it:
   ```python
   print("Hello from my conda environment!")
   ```
3. Click the **▶ Run** button in the top-right corner, or press `F5` and choose "Python File".
4. The output appears in the **terminal panel** at the bottom. You should see your message.

Notice the terminal panel shows `(myproject)` at the start of the line — that confirms VS Code is using your environment.

### Option B — Run a Jupyter notebook (`.ipynb` file)

Notebooks let you write and run code in small chunks called **cells**, and see the output right below each one. They're great for learning and for data work.

1. Create a new file called `notebook.ipynb`.
2. VS Code opens it in notebook view. In the top-right, click **Select Kernel** and choose your `myproject` environment (same idea as selecting the interpreter).
3. Click inside the first cell, type some code:
   ```python
   print("Hello from a Jupyter notebook!")
   ```
4. Press `Shift+Enter` to run the cell. The output appears right below it.
5. A new empty cell appears so you can keep going. Add another cell with `2 + 2` and run it to see the result.

> **Tip:** If you installed `pandas`, `numpy`, or `matplotlib` in Step 4, you can `import` them in any cell — as long as the notebook's kernel is set to the environment where you installed them.

### Common VS Code mistakes for beginners

- **"ModuleNotFoundError" when you try to import a package** — VS Code is probably using the wrong environment. Re-check *Select Interpreter* (for `.py` files) or *Select Kernel* (for notebooks), and make sure it points to the environment where you installed the package.
- **The Run button does nothing / errors out** — make sure you saved the file and selected an interpreter.
- **Terminal shows `(base)` instead of your environment** — open a new terminal in VS Code (**Terminal → New Terminal**); it should pick up the selected environment. If not, run `conda activate myproject` in it.


## Maintenance — Cleaning Cache & Freeing Up Space

Over time, Conda stores downloaded installer files and unused data on your computer. This is called the **cache**, and it can grow to several gigabytes. Cleaning it is safe — it does **not** delete your environments or your work. It only removes temporary files that Conda can re-download if ever needed.

### Check how much space Conda is using

```bash
conda clean --dry-run --all
```

The `--dry-run` part means "just show me what *would* be deleted, but don't actually delete anything yet." This is a safe way to preview.

### Clean everything (recommended routine cleanup)

```bash
conda clean --all
```

Type `y` when prompted. This removes:
- Cached package files (`.tar.bz2` and `.conda` downloads)
- Unused package data
- Temporary files
- Index cache

### Clean specific things only

If you want more control, you can clean one category at a time:

| Command | What it cleans |
|---------|----------------|
| `conda clean --packages` | Removes unused packages from the package cache |
| `conda clean --tarballs` | Removes cached `.tar.bz2` / `.conda` download files |
| `conda clean --index-cache` | Removes the package index cache |
| `conda clean --tempfiles` | Removes leftover temporary files |

### Clean the pip cache too

If you've used `pip` to install packages, it keeps its own separate cache:

```bash
pip cache purge
```

To just see the pip cache size without deleting:

```bash
pip cache info
```

### Recommended cleanup routine for students

Run this once every few weeks, or whenever your computer is low on disk space:

```bash
conda clean --dry-run --all      # 1. Preview what will be removed
conda clean --all                # 2. Confirm and remove it
pip cache purge                  # 3. Clear the pip cache as well
```

> **Safe to do anytime:** Cleaning the cache never touches your environments, your installed packages, or your code files. The worst case is that Conda re-downloads a file later if you reinstall something.

### Other useful maintenance commands

**Update Conda itself** to the latest version:

```bash
conda update conda
```

**Update all packages** in the currently active environment:

```bash
conda update --all
```

**Back up an environment** so you (or a classmate) can recreate it later:

```bash
conda env export > environment.yml
```

**Recreate an environment** from that backup file:

```bash
conda env create -f environment.yml
```


## Troubleshooting Common Problems

**`conda: command not found` (Mac) or `'conda' is not recognized` (Windows)**
- Windows: Make sure you opened **Anaconda Prompt**, not the regular Command Prompt.
- Mac: Close the Terminal completely and open a new window. If it still fails, run `source ~/miniconda3/bin/activate` and try again.

**My terminal doesn't show `(base)` or `(myproject)`**
- You may not have an environment activated. Run `conda activate base` to start.

**`conda install` is very slow or seems stuck**
- This is normal for the first few installs — Conda is "solving" which versions fit together. Give it a few minutes.

**I installed a package but Python says it can't find it**
- You probably installed it in the wrong environment. Run `conda env list` to check where you are, activate the correct environment, and install again.

**I think I broke an environment**
- Don't panic. Just delete it and make a new one:
  ```bash
  conda remove --name myproject --all
  conda create --name myproject python=3.12
  # Feel free to change the Python version to a newer one
  ```
  Your other environments are untouched.


## Frequently Asked Questions (FAQ)

**Q: What's the difference between Miniconda and Anaconda?**
Anaconda is the full package — it includes Conda plus hundreds of pre-installed data science packages, which makes it large (several GB). Miniconda includes only Conda and Python, so it's small and fast to install. You add packages yourself as you need them. This guide uses Miniconda because it's lighter and teaches you good habits.

**Q: What's the difference between `conda` and `pip`? Can I use both?**
Both install packages. `conda` is Conda's own installer and can handle non-Python dependencies too; `pip` is Python's standard installer and has the widest selection of packages. You *can* use both, but the safe habit is: try `conda install` first as it is maintained by community who use conda, and only use `pip install` if the package isn't available through conda. Always make sure your environment is activated first.

**Q: Do I need to create a new environment for every single project?**
For learning, it's a very good habit. Each environment keeps a project's packages isolated, so upgrading something for one project can't break another. At minimum, create one environment for this class and keep `base` clean.

**Q: I closed my terminal. Do I lose my environment?**
No. Environments are saved on your computer permanently. When you reopen the terminal, just run `conda activate myproject` again to return to it. You only lose the *activation* as when opening a terminal will usually go to `(base)`, not the environment itself.

**Q: Can I have different Python versions in different environments?**
Yes — that's one of the main benefits. One environment can use `python=3.11` and another `python=3.12`. They won't interfere with each other.

**Q: How do I update Python inside an environment?**
Activate the environment, then run `conda install python=3.12` (replace with the version you want). Note that big version jumps can sometimes require recreating the environment instead.

**Q: I'm completely lost / I think I broke everything. What now?**
Don't worry — it's hard to do permanent damage. Most problems are fixed by deleting the broken environment (`conda remove --name myproject --all`) and creating a fresh one. Your other environments stay safe. If Conda itself seems broken, you can uninstall Miniconda and reinstall it from Step 1.


**Q: Should I use the Anaconda Navigator (the graphical app) instead of typing commands?**
You can, but learning the commands is worth it — they're faster, work everywhere, and are what you'll see in most tutorials and documentation. This guide focuses on commands for that reason.

**Q: VS Code can't find my packages even though I installed them. Why?**
Almost always, VS Code is pointed at the wrong Python. Use *Python: Select Interpreter* (for `.py` files) or *Select Kernel* (for notebooks) and choose the conda environment where you actually ran `conda install`. If your environment isn't in the list, close and reopen VS Code.

**Q: What's the difference between a `.py` file and a `.ipynb` notebook?**
A `.py` file is a plain script — it runs top to bottom all at once. A `.ipynb` notebook is made of cells you run one at a time, with output shown right below each cell. Notebooks are great for learning, experimenting, and data work; scripts are better for finished programs you run repeatedly.


## Quick Command Cheat Sheet

```bash
# CHECK INSTALLATION
conda --version                              # Check Conda is installed
python --version                             # Check Python version

# ENVIRONMENTS
conda create --name NAME python=3.12         # Create a new environment
conda activate NAME                          # Enter an environment
conda deactivate                             # Leave an environment
conda env list                               # List all environments
conda remove --name NAME --all               # Delete an environment

# PACKAGES
conda install PACKAGE                        # Install a package (conda)
pip install PACKAGE                          # Install a package (pip)
conda list                                   # List installed packages

# CLEANING & MAINTENANCE
conda clean --dry-run --all                  # Preview what cleanup would remove
conda clean --all                            # Clean all caches
pip cache purge                              # Clean the pip cache
conda update conda                           # Update Conda itself
conda update --all                           # Update all packages in current env

# BACKUP & RESTORE
conda env export > environment.yml           # Save an environment to a file
conda env create -f environment.yml          # Recreate an environment from a file
```

**In VS Code, don't forget:** open your project *folder*, then use the Command Palette (`Ctrl/Cmd+Shift+P` → *Python: Select Interpreter*) — or *Select Kernel* for notebooks — to point VS Code at your conda environment.
