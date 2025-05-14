Installation
============

Requirements
------------
- Python 3.8+
- Calliope >= 0.6.6
- pandas, numpy, matplotlib, scikit-learn

Setup
-----
1. Clone the repository
2. Create and activate a virtual environment
3. Install dependencies with pip or conda

Run Example
-----------
To run a scenario for a single profile:
```bash
python run_optimization.py --profile 123 --scenario 1 --year 2023

**overview.rst**
```rst
Overview
========

This project optimizes 6617 user electricity demand profiles under five energy system scenarios using the Calliope framework.

Each profile is evaluated under:
- Two different years (e.g., 2023 and 2025)
- Five scenarios (battery only, PV+battery, PV+battery+grid, etc.)

The goal is to evaluate cost, reliability, and grid dependence for each configuration.