# Neural Network Estimation of Pickands Dependence Functions

```'link```

This repository contains the complete Python code and analysis pipeline for the paper: **"Title of the paper"**.

The project introduces and validates a novel semi-parametric methodology for estimating the Pickands dependence function of bivariate extreme value copulas using a purpose-built neural network.

## Key Features

- **Theoretically-Grounded Neural Network:** Implements a `PickandsNN` model whose architecture is based on the log-sum-exp representation for approximating convex functions.
- **Robust Post-Processing:** Includes two post-processing methods to ensure theoretical validity:
    1.  **Convex Projection (CVXPY):** A robust method to project the raw output onto the space of valid Pickands functions.
    2.  **Parameter Adjustment (Algorithm 1):** A constructive method from our theoretical framework.
- **Comprehensive Simulation Suite:** Provides code to run extensive simulations on three canonical copula families (Gumbel, Galambos, Tawn) to test the model's performance on symmetric, asymmetric, and highly flexible dependence structures.
- **Real-World Application:** Includes a full, end-to-end case study on real-world climatological data from Météo-France to analyze the spatial dependence of extreme soil dryness.

## Methodology Overview

The core of this project is a semi-parametric pipeline for estimating the Pickands function $A(t)$:

1.  **Marginal Distribution Modeling:** For real-world data, the margins are first transformed into uniform pseudo-observations using a semi-parametric approach that combines the empirical CDF with a **Generalized Pareto Distribution (GPD)** for the tails. This is a critical step in modern Extreme Value Theory.

2.  **Training Target Generation:** From the uniform pseudo-observations $(U, V)$, we compute the angular coordinates $t$ and a non-parametric estimate of the Pickands function $\hat{A}(t)$. This noisy but unbiased estimate serves as the training target for the neural network.

3.  **Neural Network Training:** The `PickandsNN` model is trained to learn a smooth, regularized version of the noisy empirical target. The training process uses an **adaptive penalty term**, where the penalty weight $\lambda$ is dynamically adjusted based on the estimated strength of dependence, which proved crucial for achieving stable convergence.

4.  **Convex Projection:** The raw output of the network is projected using CVXPY to guarantee that the final estimate is convex and satisfies the theoretical bounds of a valid Pickands function. Our results consistently show this step to be essential for both accuracy and stability.

## Installation

To run this project, follow these steps. It is highly recommended to use a virtual environment.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repository-name.git
    cd your-repository-name
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install the required packages:**
    A `requirements.txt` file is provided. Install it using pip:
    ```bash
    pip install -r requirements.txt
    ```
    *If you do not have a `requirements.txt` file, you can create one from the environment where you developed the code by running `pip freeze > requirements.txt`.*

## How to Run the Analysis

The entire analysis is contained within the `analysis.ipynb` Jupyter Notebook.

1.  **Launch Jupyter:**
    ```bash
    jupyter lab
    ```
    or
    ```bash
    jupyter notebook
    ```

2.  **Open `analysis.ipynb`** and run the cells in order from top to bottom.

## Project Structure

The repository is organized as follows to ensure clarity and reproducibility:

```.
├── SWI_Package_1969-2024/   # Data folder for raw Météo-France CSVs (should be added to .gitignore)
│
├── figures/                   # Directory for saved plots and figures from the analysis.
│
├── simulation_results_multicopula_adapted_lambda.csv                   # simulation output CSV.
│
├── analysis.ipynb             # The main Jupyter Notebook containing all code, analysis, and visualizations.
│
├── requirements.txt           # A list of all Python packages required to run the code.
│
├── .gitignore                 # Specifies files and folders for Git to ignore (e.g., data, virtual env).
│
└── README.md                  # This file, providing an overview of the project.
```
- **`analysis.ipynb`**: This is the central file of the project. It contains all the Python code for the simulations, the real-data application, and generates all the figures and tables presented in the paper.
- **`SWI_Package_1969-2024/`**: This folder is intended to hold the raw `.csv` files from Météo-France. As it contains large data files, it is recommended to add it to your `.gitignore` file.
- **`figures/` and `simulation_results_multicopula_adapted_lambda.csv `**: The folder and this file are automatically created (if they don't exist) by the notebook to store the outputs, keeping the project organized.
- **`requirements.txt`**: This file allows anyone to replicate the exact Python environment used for this analysis by running `pip install -r requirements.txt`.
## Reproducing the Results

To reproduce the results presented in the paper:

1.  **Simulations:** Simply run the cells in the "Simulation Study" section of `analysis.ipynb`. The script will generate the data, run the simulations, save the results to a CSV file in the `results/` directory, and generate the summary plots.

2.  **Real-Data Application:**
    - Download the SWI dataset from Météo-France and place the `.csv` files into a folder named `SWI_Package_1969-2024` in the root of the project directory.
    - Run the cells in the "Application to Real-World Data" section of `analysis.ipynb`.

## Citing this Work

If you use this code or methodology in your research, please cite our paper:

```bibtex
@article{Lopez_PickandsNN_2025,
  title   = {Title of the paper},
  author  = {Lopez, Olivier},
  journal = {Journal Name}, 
  year    = {2025},         
  volume  = {XX},
  pages   = {XX--XX}
}
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
