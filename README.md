# Heart Disease Bayesian Network Analysis
This project analyzes a heart disease dataset using a Bayesian Network. The goal is to explore the relationships between various health factors and the presence of heart disease and to build a probabilistic model that can be used for inference.

## Project Structure
The main analysis is performed within a Jupyter notebook.

## Setup and Installation
To run this project, you will need to have Python and Jupyter Notebook installed. You can install the necessary libraries using pip:
```bash
pip install pandas pgmpy
```

## Data
The dataset used in this project is the Heart Disease dataset, which is publicly available on GitHub. The notebook directly downloads the data from this source.

## Analysis
The Jupyter notebook performs the following steps:

Data Loading and Initial Exploration: The dataset is loaded into a pandas DataFrame, and initial checks are performed to understand the data's structure, content, and basic statistics.\
Data Cleaning: Missing values are handled by dropping rows with any missing information. Duplicate rows are also identified and removed.\
Feature Engineering: Several continuous features (age, chol, thalach) are converted into categorical features by binning their values into predefined ranges.\
Bayesian Network Modeling: A Bayesian Network is defined with specific dependencies between the variables. This structure represents assumed probabilistic relationships.\
Model Training: The Bayesian Network model is trained using the cleaned and processed data. The Maximum Likelihood Estimator is used to learn the conditional probability distributions (CPDs) for each node in the network.\
Inference: The trained Bayesian Network is used to perform probabilistic inference. Specifically, the notebook demonstrates querying the model to find the probability of heart disease (target) given specific evidence about other health factors (age, fbs, chol, thalach).\
Saving Processed Data: The cleaned and feature-engineered dataset is saved as a new CSV file (heart_disease.csv) for potential future use.
## Running the Notebook
Clone this repository (if applicable) or ensure you have the Jupyter notebook file.
Open a terminal or command prompt.
Navigate to the directory where the notebook is saved.
Start Jupyter Notebook: jupyter notebook
Open the notebook file (e.g., heart_disease_analysis.ipynb) in your web browser.
Run the cells in the notebook sequentially.
## Dependencies
-pandas
-pgmpy
