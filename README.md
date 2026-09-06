# Car Price Prediction

A beginner-friendly machine-learning project that estimates a used car's selling price from its year, current price, mileage, fuel type, seller type, transmission, and ownership history. The complete exploratory analysis, preprocessing workflow, model training, evaluation, and plots are contained in the accompanying Jupyter notebook.

## Project highlights

- Uses a dataset of **301 used-car listings** stored locally in CSV format.
- Checks the dataset structure, summary statistics, categorical-value distributions, and missing values.
- Converts categorical features to numeric values before training.
- Trains and compares **Linear Regression** and **Lasso Regression** models.
- Evaluates each model with the coefficient of determination ($R^2$) on an 80/20 train/test split.
- Visualizes actual selling prices against predicted prices for both training and test data.

## Repository structure

```text
.
├── car_price_prediction.ipynb   # Analysis, training, evaluation, and visualizations
├── sample_data/
│   └── car data.csv             # Input dataset (301 rows, 9 columns)
└── README.md
```

## Dataset

The model predicts `Selling_Price`. The notebook drops `Car_Name` and uses the remaining columns below as features.

| Column | Description | Role |
| --- | --- | --- |
| `Car_Name` | Name/model of the car | Excluded from training |
| `Year` | Manufacturing year | Feature |
| `Selling_Price` | Observed resale price | Target |
| `Present_Price` | Current showroom price | Feature |
| `Kms_Driven` | Total distance driven | Feature |
| `Fuel_Type` | Petrol, Diesel, or CNG | Encoded feature |
| `Seller_Type` | Dealer or Individual | Encoded feature |
| `Transmission` | Manual or Automatic | Encoded feature |
| `Owner` | Number/category of previous owners | Feature |

The dataset included in this repository has no missing values. Prices use the units provided by the source CSV; confirm the appropriate currency and scale before using predictions in a real-world decision.

### Categorical encoding

The notebook uses the following ordinal mappings:

| Feature | Mapping |
| --- | --- |
| `Fuel_Type` | `Petrol` → `0`, `Diesel` → `1`, `CNG` → `2` |
| `Seller_Type` | `Dealer` → `0`, `Individual` → `1` |
| `Transmission` | `Manual` → `0`, `Automatic` → `1` |

> These mappings are implementation details, not rankings. For a production model, consider one-hot encoding nominal categories to avoid implying an order.

## Requirements

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`

## Getting started

1. Clone the repository and move into it:

   ```bash
   git clone <repository-url>
   cd car_prediction_model
   ```

2. Create and activate a virtual environment (recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate          # macOS/Linux
   # .venv\Scripts\activate           # Windows PowerShell
   ```

3. Install the required packages:

   ```bash
   python -m pip install --upgrade pip
   python -m pip install pandas numpy matplotlib seaborn scikit-learn notebook
   ```

4. Start Jupyter and open the notebook:

   ```bash
   jupyter notebook car_price_prediction.ipynb
   ```

5. Run all cells from top to bottom. Run Jupyter from the repository root so the relative dataset path, `./sample_data/car data.csv`, resolves correctly.

## Workflow

1. Load `sample_data/car data.csv` with pandas.
2. Inspect the shape, sample rows, descriptive statistics, data types, null counts, and category distributions.
3. Encode fuel type, seller type, and transmission.
4. Create the feature matrix `X` and target vector `Y` (`Selling_Price`).
5. Split the data into training and test sets with `test_size=0.2` and `random_state=2`.
6. Fit Linear Regression and Lasso Regression models.
7. Calculate $R^2$ scores and plot actual versus predicted prices for each model.

## Results in the notebook

The notebook's saved run reports the following $R^2$ scores:

| Model | Training $R^2$ | Test $R^2$ |
| --- | ---: | ---: |
| Linear Regression | 0.8838 | 0.8402 |
| Lasso Regression | 0.8436 | 0.8497 |

Results can change if you modify the dataset, feature processing, split configuration, or library versions. These scores are useful as a learning-project baseline and should not be treated as a production validation result.

## Limitations and next steps

- The dataset is small, so a single train/test split provides only a limited estimate of generalization performance.
- `Car_Name` is excluded; extracting make/model features may improve accuracy.
- The notebook does not persist a trained model or expose a prediction API.
- Add cross-validation, hyperparameter tuning, residual/error analysis, and a held-out validation strategy before comparing models for deployment.
- Keep preprocessing and inference together in a scikit-learn pipeline to ensure new data receives identical transformations.

## License

No license has been specified for this repository. Add a license file before redistributing or using the project beyond its intended context.
