# Candidates Pipeline

This project contains a Jupyter notebook that reads candidate records from a semicolon-delimited CSV file, loads the data into PostgreSQL, queries candidates who meet the notebook's interview score threshold, and creates charts summarizing hires.

## Requirements

- Python 3.13 (the notebook kernel metadata specifies Python 3.13.7)
- Jupyter Notebook or JupyterLab to open and run `pipeline/etl.ipynb`
- Python packages imported by the notebook: `pandas`, `matplotlib`, `seaborn`, `SQLAlchemy`, and `psycopg2` (the PostgreSQL driver)
- Docker to run PostgreSQL 16

Install the Python packages in the environment used by your Jupyter kernel. No dependency manifest is currently included in the project.

## Start PostgreSQL 16 with Docker

Run this command in PowerShell:

```powershell
docker run --name postgres_db `
 -e POSTGRES_USER=postgres `
 -e POSTGRES_PASSWORD=1234 `
 -e POSTGRES_DB=candidates_db `
 -p 5432:5432 `
 -d postgres:16
```

The notebook connects to PostgreSQL at `localhost:5432` using the database and credentials configured above.

## Run the notebook

1. Start the PostgreSQL container using the command above.
2. Open `pipeline/etl.ipynb` in Jupyter.
3. Run the notebook with the project Python environment. Its CSV reader uses the relative path `../data/candidates.csv`, so start the notebook with `pipeline` as the working directory (or adjust the path if your Jupyter setup uses a different working directory).

The notebook replaces the `candidates` table when it loads the CSV, then queries that table and displays hiring summary charts.
