# Book Recommendation System

A collaborative-filtering and learning-to-rank research project built with the **Book-Crossing dataset**, **Apache Spark MLlib**, and **XGBoost**. The notebook prepares user–book interactions, engineers user and item features, tunes multiple recommendation approaches, and compares their top-`K` ranking performance.

## Methods

The experiment compares three recommendation models:

- **ALS (Alternating Least Squares):** matrix-factorization collaborative filtering using Spark MLlib.
- **Factorization Machines (FMRegressor):** feature-based interaction modelling using Spark MLlib.
- **XGBRanker:** gradient-boosted learning-to-rank using XGBoost.

The notebook includes data loading, filtering, feature engineering, train/validation/test splitting, hyperparameter tuning, final evaluation, and ranking metrics such as NDCG@K, MAP@K, Precision@K, Recall@K, and catalog coverage.

## Repository structure

```text
book_recommender/
├── data/
│   ├── raw/
│   │   ├── BX_Books.csv
│   │   ├── BX-Users.csv
│   │   └── BX-Book-Ratings.csv
│   └── README.md
├── notebooks/
│   └── book-recommender-system.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

- `data/raw/`: source CSV files used by the experiment.
- `notebooks/`: exploratory and modelling workflow.
- Generated Spark checkpoints and model artifacts are kept out of version control.

## Dataset

The project uses the Book-Crossing data files:

| File | Contents |
|---|---|
| `BX_Books.csv` | Book metadata |
| `BX-Users.csv` | User demographic information |
| `BX-Book-Ratings.csv` | User–book ratings |

The notebook reads these semicolon-delimited files using ISO-8859-1 encoding. Review the dataset's original terms and attribution requirements before redistributing the data.

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/ukrumpa/book_recommender.git
cd book_recommender
```

### 2. Create an environment

Python 3.12 and Java 17 or later are recommended for the pinned PySpark 4.x dependency.

```bash
python -m venv .venv
```

Activate it:

- Windows PowerShell: `.venv\Scripts\Activate.ps1`
- macOS/Linux: `source .venv/bin/activate`

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the notebook

```bash
jupyter lab
```

Open `notebooks/book-recommender-system.ipynb` and run the cells from top to bottom. The notebook resolves the dataset from `data/raw/` relative to the repository, so it is no longer tied to a Kaggle input directory.

## Experiment configuration

The notebook defines the main experiment settings near the beginning, including ALS parameters, user-rating filters, a 25,000-row model-comparison sample target, a 70/15/15 train/validation/test split, and a top-10 ranking evaluation cutoff. Adjust these settings there when running a new experiment.

## Reproducibility notes

- Run the notebook from a clean environment and execute cells in order.
- The workflow uses Spark locally (`local[*]`) and may require substantial memory depending on the dataset and machine.
- Model artifacts and Spark checkpoint files are generated at runtime; they are intentionally excluded from Git.
- Results depend on the data split, filtering thresholds, software versions, and runtime configuration.

## Limitations

This is an experimental recommendation-system project, not a production recommendation service. The notebook is the current source of truth for implementation details. A future iteration could extract reusable data, training, and evaluation functions into a dedicated `src/` package and add automated tests.

## License

No software license is currently declared for this repository. Unless a license is added, the default copyright restrictions apply to reuse of the project code. Dataset terms are separate and must also be respected.
