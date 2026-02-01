# VeloStat: High-Performance COVID-19 Analytical Pipeline
<img width="644" height="347" alt="COVIED" src="https://github.com/user-attachments/assets/428a9e8e-18c0-4cbb-b911-485634a5d197" />

A modular data engineering and analytics suite designed to process, normalize, and analyze global epidemiological time-series data. This project demonstrates advanced **NumPy-vectorized computation** and **Object-Oriented ETL** patterns, moving away from inefficient iterative processing.

# Engineering Architecture

The system is decoupled into three distinct layers to ensure scalability and maintainability:

- **Ingestion Layer:** Standardizes disparate JHU CSSE time-series datasets into a unified schema.
- **Processing Engine:** Implements O(n) complexity growth-rate calculations using NumPy vectorization.
- **Visualization Layer:** Generates 7-day smoothed trend analysis to filter weekend reporting noise.

# Tech Stack & Tools

- **Core:** Python 3.8+
- **Data Engine:** Pandas (Optimized DataFrames), NumPy (Vectorized Arrays)
- **Math:** SciPy/NumPy Convolution (for Signal Smoothing)
- **Environment:** Scoped virtual environments with decoupled data directories.

# Key Engineering Features

1. Vectorized Growth Velocity
Unlike legacy scripts that use `iterrows()` or manual loops, this engine utilizes `np.diff()` for instantaneous delta calculations across millions of rows.

2. Signal Smoothing (7-Day MA)
To handle the "weekend lull" in global reporting, the pipeline applies a 1D convolution window:
$$y[n] = \frac{1}{N} \sum_{j=0}^{N-1} x[n-j]$$
This results in a stabilized trendline that accurately reflects pandemic acceleration.

3. Idempotent ETL Pipeline
The logic is designed to be **Idempotent**—running the scripts multiple times will always yield the same consistent state, preventing data duplication or header collision.

# Execution & Setup

1. **Initialize Environment:**

   python -m venv venv
   source venv/bin/activate  # venv\Scripts\activate on Windows
   pip install -r requirements.txt
