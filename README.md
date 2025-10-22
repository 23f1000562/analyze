# Data Processing Application

This repository hosts a simple yet robust data processing application, demonstrating Python scripting with Pandas, static site serving with Tailwind CSS, and a comprehensive CI/CD pipeline using GitHub Actions.

## Project Structure

*   `.github/workflows/ci.yml`: GitHub Actions workflow for linting, data processing, and deployment.
*   `execute.py`: A Python script that processes `data.csv` and outputs `result.json`.
*   `data.csv`: The primary data source, converted from the original `data.xlsx`.
*   `index.html`: A single-file responsive web page using Tailwind CSS, providing an overview of the project.
*   `LICENSE`: The MIT License text.

## `execute.py` - Fixed and Enhanced

The `execute.py` script is designed to read structured data, perform aggregations, and output the result in JSON format. A non-trivial error, such as a `TypeError` due to mixed data types in a numeric column, has been fixed by employing `pd.to_numeric` with `errors='coerce'` and `fillna(0)`. This ensures robust data handling, even if the 'Value' column contains non-numeric entries, making the script resilient and reliable.

**Key Features:**
*   Reads `data.csv` using Pandas.
*   Robustly converts the 'Value' column to a numeric type, handling potential errors gracefully.
*   Groups data by 'Category' and sums the 'Value' column.
*   Outputs the aggregated data as a pretty-printed JSON string.
*   Ensured compatibility with Python 3.11+ and Pandas 2.3.

## `data.csv` - Data Source

`data.xlsx` was converted to `data.csv` to serve as the standardized input for `execute.py`. This ensures consistent data handling across environments. The committed `data.csv` contains the following sample data:

```csv
Category,Value,Date
A,100,2023-01-01
B,150,2023-01-02
A,200,2023-01-03
C,50,2023-01-04
B,250,2023-01-05
A,300,2023-01-06
```

## Getting Started

### Prerequisites

Ensure you have Python 3.11+ installed. You can install the required Python packages using pip:

```bash
pip install pandas==2.3 ruff
```

### Local Usage

1.  **Run the Python script:**
    ```bash
    python execute.py > result.json
    ```
    This will execute the data processing logic and save the output to `result.json`.

2.  **View the web page:**
    Open `index.html` in your web browser.

## CI/CD with GitHub Actions

The `.github/workflows/ci.yml` file defines a GitHub Actions workflow that automates several crucial steps:

*   **Trigger:** Runs on every `push` to the `main` branch and can be manually dispatched.
*   **Linting (Ruff):** Checks Python code for style violations and potential errors using `ruff`.
*   **Data Processing:** Executes `python execute.py` and redirects its output to `public/result.json`. This `result.json` is **not committed** to the repository; it is generated dynamically during CI.
*   **GitHub Pages Deployment:**
    *   `result.json` is packaged as an artifact.
    *   This artifact is then published to GitHub Pages.
    *   You can access the generated `result.json` directly via your GitHub Pages URL (e.g., `https://<YOUR_USERNAME>.github.io/<YOUR_REPOSITORY>/result.json`).

This workflow ensures code quality and keeps the generated `result.json` always up-to-date and publicly accessible via GitHub Pages.

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.