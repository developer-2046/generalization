# Scaling Laws and Generalization Phase Transitions

This project contains the code and analysis pipeline for a research study investigating the emergence of generalization phase transitions in different neural network architectures as a function of data and model scale.

## Project Structure

.
├── data_json/              # Input: Raw JSON results from experiments
│   ├── gpu_scaling_results-1.json
│   └── ...
├── data_csv/               # Output: Processed CSV data
│   ├── run_1.csv
│   ├── ...
│   └── all_runs_combined.csv
├── statistical_analysis/   # Output: Aggregated statistical results
│   └── statistical_summary.csv
├── visualizations/         # Output: Publication-quality plots
│   ├── validation_loss_scaling.png
│   └── ...
├── experiment.py           # The main script to run the PyTorch experiments
├── preprocessing.ipynb     # Notebook to process JSON -> CSV
├── analysis.ipynb          # Notebook to perform statistical analysis
└── visualization.ipynb     # Notebook to create plots## Workflow

The analysis is performed in three main stages, using the provided Jupyter notebooks. Please run them in the following order:

### 1. Run the Experiment

First, run the main PyTorch experiment script (`experiment.py` from our previous discussion) multiple times (e.g., 5 times). Ensure the output JSON files are saved in the `data_json/` directory with the naming convention `gpu_scaling_results-n.json`, where `n` is the run number.

### 2. Pre-processing (`preprocessing.ipynb`)

This notebook is the first step in the analysis pipeline. It performs the following actions:
- Scans the `data_json/` directory for all experiment result files.
- Parses each nested JSON file and flattens it into a structured table (a pandas DataFrame).
- Saves the data from each experimental run into its own separate CSV file inside the `data_csv/` folder (e.g., `run_1.csv`).
- Combines the data from all runs into a single, master CSV file: `data_csv/all_runs_combined.csv`.

### 3. Statistical Analysis (`analysis.ipynb`)

This notebook takes the combined data and prepares it for visualization by computing summary statistics.
- Loads the `all_runs_combined.csv` file.
- Groups the data by experimental conditions (architecture, model size, dataset size).
- For each group, it calculates the **mean** and **standard deviation** of the key performance metrics (`val_loss`, `gen_gap`, `training_time`, etc.).
- Saves the resulting summary table to `statistical_analysis/statistical_summary.csv`.

### 4. Visualization (`visualization.ipynb`)

This is the final step, where we generate publication-quality plots from the aggregated data.
- Loads the `statistical_summary.csv` file.
- Creates the primary plot for the paper: **Validation Loss vs. Dataset Size**, showing the mean performance with shaded error bands representing the standard deviation. This plot is designed to clearly visualize the phase transition phenomenon.
- Generates secondary plots, such as **Generalization Gap vs. Dataset Size**, to provide additional insights.
- Saves all generated plots as high-resolution PNG files in the `visualizations/` folder.
