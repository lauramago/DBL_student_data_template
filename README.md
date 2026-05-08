# 🚀 DBL Student Project Template

This guide is meant for students joining the DBL.  

Follow the instructions and contact your supervisor or [laugon@dtu.dk](mailto:laugon@dtu.dk) if you have any questions :)

Welcome new student!

---

## Before you start
As a member of the DBL, you have a **DTU ID** that can look like `laugon` or 's252456'. It matches your DTU email address.
You are expected to save your project's data in this DBL SharePoint folder before you leave: https://dtudk.sharepoint.com/:f:/s/DigitalBiotechnologyHub/IgDuPg7OM6jOR53D1LPQfIqIAcOzrtK1XqqaNNr9yY966ec?e=GpAaTv

Depositting your data here is a prerequisite for you to getting your final grade :)
Please, follow the folder structure shown in this repo, detailed below.

## Folder structure
```bash
project_name/
├── README.md             # Overview and clear instructions on how to run
├── LICENSE               # (if open source or shared)
├── environment.yml       # or requirements.txt / pyproject.toml
├── data/                 # Raw or processed data (usually .gitignored)
│   ├── raw/              # Untouched data
├── notebooks/            # Jupyter/Colab notebooks for exploration
├── src/                  # Reusable code (functions, classes, modules) "shelf"
│   ├── __init__.py
│   ├── config.py
│   ├── preprocessing.py
│   └── plotting.py      
│   └── utils/            # Reusable helper functions
├── scripts/              # sequential pipeline steps "recipe"
│   ├── 00_sumbit.sh
│   ├── 01_preprocess.py
│   ├── 02_train.py
│   └── 03_plot_results.py
├── tmp/                  # Unit tests / experiment validation
├── results/              # Outputs (figures, logs, metrics)
│   ├── figures/
│   └── logs/
└── docs/                 # Project documentation (.ppt, posters, manuscripts)
```

## Recommended naming convention for scripts and results

The numbering of files in `scripts/` should match the **order of the pipeline** (just like following a recipe).  
- Example: `01_preprocess.py` → run first, then `02_train.py` → run second, etc.

All outputs generated in the `results/` folder should also include the **same step number** in their filenames.  
This makes it clear **which script produced which result** (see example below).

### Example pipeline recommendations
```bash
Scripts:
scripts/
├── 00_sumbit.sh
├── 01_preprocess.py
├── 02_train.py
└── 03_plot_results.py
```

Results:
```bash
results/
├── 01_preprocess_summary.json # created by 01_preprocess.py
├── 02_model.pkl # created by 02_train.py
└── 03_training_curve.png # created by 03_plot_results.py
```

## Running the full pipeline

Each script in `scripts/` is designed as one step in your workflow (like steps in a recipe).  
- Scripts are **numbered** to indicate their order.  
- Outputs in `results/` should also use the same number prefix so it’s clear which step generated them.  

To make it easier to run everything in one go, you can add a **master script** called `run_pipeline.py`.  
This script will automatically execute all numbered scripts in `scripts/` in the correct order.


### Example `run_pipeline.py`
```python
import subprocess
import os
import glob

def run_pipeline():
    # find all numbered scripts
    steps = sorted(glob.glob(os.path.join("scripts", "[0-9][0-9]_*.py")))
    for step in steps:
        print(f"\n🚀 Running {step} ...")
        subprocess.run(["python", step], check=True)

if __name__ == "__main__":
    run_pipeline()
```

## Notes

Use /tmp as a sandbox for scratch or temporary files. This avoids cluttering your project directories with intermediate junk. :)

We advise you to use version control with Git. Use the provided .gitignore file to manage which files should (and shouldn’t) be pushed to GitHub. Typically, you should never push raw data or large result files — only code and configs. If in doubt, ask your supervisor before committing data or outputs.

Welcome to the DBL! We hope you have a lot of fun doing science with us.




