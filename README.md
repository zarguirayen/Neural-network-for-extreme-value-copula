# Neural-network-for-extreme-value-copula
This repository contains the complete Python code and analysis pipeline for the paper. The project introduces and validates a novel semi-parametric methodology for estimating the Pickands dependence function of bivariate extreme value copulas using a purpose-built neural network.
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
