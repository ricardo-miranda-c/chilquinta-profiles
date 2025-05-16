Installation
============

Requirements
------------
1. The Python programming language, version 3.8 or 3.9.
2. A number of Python add-on modules (see below for the complete list).
3. A solver: Calliope has been tested with CBC, GLPK, Gurobi, and CPLEX. Any other solver that is compatible with Pyomo should also work.
4. The Calliope software itself.

How to use
-----
1. Clone the repository:

.. code-block:: bash

    git clone https://mygit.th-deg.de/tcf-geo/chilquinta_model.git

2. Install the required packages:
3. Set up the Gurobi solver:
4. Run the model:
   

**Initial Setup**

Ensure all necessary dependencies are installed and that configurations in :ref:`locations.yaml <locations>`, :ref:`techs.yaml <techs>`, and :ref:`model.yaml <model>` are tailored to your needs.

**Running Models**

- Navigate to the corresponding directory (e.g., ``scripts_run``).
- To run all scenarios for a year:

``python run_all.py``

**Extracting Results**

Use the ``extract_all.py`` script in the scripts_extract folder to extract result once the ``run_all.py`` file is done.

**Cleaning Results**

Delete previous results with:

``python delete_results.py``

Scripts
-----------

run_all.py
~~~~

**Includes scripts to manage executions:**
   - delete_results.py: Deletes previous results of every year for each scenario.
   - run_all.py: Executes all models for both years of every scenarios.

Documentation for run_all.py in scripts_run (General Execution Script)

The run_all.py script automates the execution of all scenarios across the years 2024 and 2025.
Below is an explanation of its workflow:

.. code-block:: python

    import subprocess

    folders = ['2024', '2025']
    files = ['E1/run_all.py', 'E2/run_all.py', 'E3/run_all.py', 'E4/run_all.py', 'E5/run_all.py']

    processes = []

    for folder in folders:
        for file in files:
            full_path = f"{folder}/{file}"
            process = subprocess.Popen(['python', full_path])
            processes.append(process)
    for process in processes:
        process.wait()

    print("All Python files have been executed.")

**Purpose:** Executes the run_all.py scripts located in each scenario folder (E1 to E5) for both 2024 and 2025.

- **Workflow:**

  - Loops through the folders list (2024 and 2025).
  - Iterates over the files list, which contains the relative paths of the run_all.py scripts in each scenario.
  - For each combination of folder and file, constructs the full path and starts a subprocess to execute the script.
  - Waits for all processes to complete before printing a success message.
  
- **Output:** Confirms that all scripts have been executed successfully.


run_all_model.py
~~~~

.. code-block:: python

    import os
    import subprocess

    carpeta_relativa = "2024/E1/batch_files"
    carpeta = os.path.join(os.getcwd(), carpeta_relativa)

    os.makedirs(carpeta, exist_ok=True)

    print(f"folder: {carpeta}")
    procesos = []

    for archivo in os.listdir(carpeta):
        if archivo.endswith(".bat"):
            ruta_archivo = os.path.join(carpeta, archivo)
            print(f"Starting: {ruta_archivo}")
            proceso = subprocess.Popen([ruta_archivo], shell=True)
            procesos.append(proceso)

    for proceso in procesos:
        proceso.wait()

    print("All clear.")

delete_results.py
~~~~

.. code-block:: python

    import os
    import shutil

    main_folders = ['2024', '2025']

    target_folder = 'results'

    for main_folder in main_folders:
        for folder, subfolders, files in os.walk(main_folder, topdown=False):
            for subfolder in subfolders:
                if subfolder == target_folder:
                    folder_to_delete_path = os.path.join(folder, subfolder)
                    shutil.rmtree(folder_to_delete_path)

                    print(f'The folder {subfolder} has been deleted in {folder}.')