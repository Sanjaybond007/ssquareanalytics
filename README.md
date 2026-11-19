# S-Square Analytics — Cart Abandonment & Product Recommendation

A Flask web application that combines **cart-abandonment prediction and analysis** with a **content-based product recommendation system**. It provides a dashboard for exploring customer activity data, scoring uploaded datasets with a trained classifier, reviewing evaluation metrics, and finding similar products using TF-IDF and cosine similarity.

## Features

### Cart-abandonment analytics
- Upload customer activity datasets in CSV, XLSX, or XLS format.
- Load the bundled classification model or upload a compatible model file (`.pkl`, `.pickle`, `.sav`, or `.bin`).
- Predict cart-abandonment probabilities for individual records or complete datasets.
- Adjust the decision threshold used to classify a customer as likely to abandon a cart.
- Optionally apply `log1p` transformation to model features.
- Explore dataset previews and feature distributions.
- When the uploaded dataset contains the `Cart_Abandoned` target column, view classification metrics and visualizations, including ROC and precision–recall curves, a confusion matrix, and a classification report.
- Download scored results as a CSV file.

### Product recommendations
- Select a product from the catalogue in `products.csv`.
- Generate up to six similar-product recommendations.
- Uses product title, category, and description text with TF-IDF vectorization and cosine similarity.
- Displays product information including category, price, description, and similarity score.

## Tech Stack

- **Backend:** Python, Flask
- **Data processing:** Pandas, NumPy
- **Machine learning:** scikit-learn
- **Visualizations:** Plotly
- **Frontend:** HTML, CSS, JavaScript
- **Data formats:** CSV, XLSX, XLS

## Project Structure

```text
s-square-flask/
├── app.py
├── recommender.py
├── products.csv
├── train_classifier.pkl
├── requirements.txt
├── templates/
│   ├── base.html
│   ├── index.html
│   └── recommender.html
├── static/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── ux.js
├── uploads/       # Uploaded datasets (created/used by the app)
└── outputs/       # Scored CSV output (created/used by the app)
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Sanjaybond007/s-square-flask.git
cd s-square-flask
```

If your GitHub repository uses a different name, replace the URL and folder name with your repository's actual details.

### 2. Create and activate a virtual environment

**Windows (Command Prompt):**

```cmd
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the application

```bash
python app.py
```

Open the local URL shown in the terminal, usually:

```text
http://127.0.0.1:5000
```

The product recommender is available at `/recs`.

## Using the Application

### Cart-abandonment dashboard
1. Open the home page.
2. Use the bundled model if `train_classifier.pkl` loads successfully, or upload a compatible model.
3. Upload a customer activity dataset.
4. Use the available controls to make a single prediction or score the uploaded dataset.
5. Review the probability scores, predictions, and available visualizations.
6. Download the scored CSV when processing is complete.

The default feature names used when a model does not expose feature names are:

- `No_Items_Added_InCart`
- `No_Checkout_Confirmed`
- `No_Checkout_Initiated`
- `No_Customer_Login`
- `No_Page_Viewed`

The expected target column for evaluation is `Cart_Abandoned`. For meaningful evaluation metrics, include this target column with binary values such as `0` and `1` (or supported yes/no values).

### Product recommender
1. Navigate to `/recs`.
2. Choose a product from the catalogue.
3. Submit the selection to see similar products.

The `products.csv` file must contain these columns: `id`, `title`, `category`, `description`, and `price`. The recommender also supports some common aliases for product ID, title, and description columns.

## Input and Output Files

- **Model:** `train_classifier.pkl` — a serialized scikit-learn-compatible classifier. Only load model files from trusted sources.
- **Product catalogue:** `products.csv` — required for product recommendations.
- **Uploaded data:** CSV, XLSX, or XLS files.
- **Scored output:** `outputs/scored_cart_abandonment.csv`.

The application creates the `uploads/` and `outputs/` directories as needed.

## Important Notes

- Do **not** commit your virtual environment (`venv/` or `.venv/`), secrets, or local environment files to GitHub.
- Uploaded datasets may contain customer information. Use appropriately anonymized data and do not publish sensitive records in a public repository.
- The application currently uses a development Flask configuration. Before production deployment, configure a secure secret key, disable debug mode, add upload-size limits and appropriate validation, and review authentication and data-protection requirements.
- Pickle-based model files can execute code when loaded. Load only trusted model files.
- Model performance depends on the training data, preprocessing, feature order, and compatibility between the model and uploaded data.

## Requirements

Dependencies are listed in `requirements.txt`. The current file pins Flask, Pandas, NumPy, scikit-learn, Plotly, and openpyxl.

## Contributors

- Sanjay B

## License

No license is specified in this repository. Add a `LICENSE` file if you intend to distribute the project for reuse.
