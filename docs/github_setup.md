# Uploading This Project to GitHub

## Option 1: GitHub website

1. Sign in to GitHub and select **New repository**.
2. Name it `scoliosis-angle-reliability`.
3. Add a short description, such as: `Independent analysis of agreement among manual, spline-based, and neural-network-assisted scoliosis angle measurements.`
4. Choose **Public** only when you are comfortable sharing the code and written work. A private repository is fine while the project is developing.
5. Do not ask GitHub to create another README or `.gitignore`, because those files are already included.
6. Create the repository and follow GitHub's instructions for pushing an existing repository.

## Option 2: Terminal

Run these commands from inside the project folder after replacing `<YOUR-USERNAME>`:

```bash
git init -b main
git add .
git commit -m "Add Week 1 data cleaning and EDA"
git remote add origin https://github.com/<YOUR-USERNAME>/scoliosis-angle-reliability.git
git push -u origin main
```

Before committing, confirm that the raw and processed CSV files are excluded:

```bash
git status
```

Files inside `data/raw/` and `data/processed/` should not appear, except for the `.gitkeep` placeholders and `data/README.md`.

## Suggested weekly workflow

```bash
git status
git add .
git commit -m "Document Week 2 curve matching"
git push
```

Use a short commit message that says what changed. Do not commit a result you do not yet understand; update the notebook explanation alongside the code.
