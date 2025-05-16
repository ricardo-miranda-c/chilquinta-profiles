Model Structure
===============

This section describes the structure of the model, including the organization of the files and folders
used in the model. The model is designed to be flexible and modular, allowing for easy modifications
and updates. The structure is organized into different folders, each containing specific
files related to the model's configuration, data, and scenarios.
The model is organized into a series of folders and files, each serving a specific purpose. The main folders include:


- **model_config**: Contains configuration files for the model, including technology definitions and location data.
- **timeseries_data**: Contains time series data files used in the model, such as demand profiles and generation data.
- **scenarios**: Contains scenario files that define different configurations and assumptions for the model runs.

.. code-block:: text

    2024
        E1
            model_config
                locations.yaml
                techs.yaml
            timeseries_data
                5kwh_2024.csv
                timeseries.csv
            model.yaml
            scenarios_E1_G1.yaml
            scenarios_E1_G2.yaml
            scenarios_E1_G3.yaml
        E2
        E3
        E4
        E5
    2025

model_config
--------

.. _locations:

locations.yaml
~~~~

.. code-block:: yaml

    locations:
        demand:
            coordinates: {lat: 40, lon: 20}

------------

.. _techs:

techs.yaml
~~~~

.. code-block:: yaml

    techs:

        power_supply_G1:
            essentials:
                name: 'National Power Supply'
                color: '#C5ABE3' 
                parent: supply
                carrier: electricity
            constraints:
                resource: inf
                lifetime: 40
            costs:
                monetary:
                    interest_rate: 0.10
                    om_con: 0.3531   
                    om_annual: 0.075 #USD/kWh/year
        power_supply_G2:
            essentials:
                name: 'National Power Supply'
                color: '#C5ABE3'
                parent: supply
                carrier: electricity
            constraints:
                resource: inf
                lifetime: 40
            costs:
                monetary:
                    interest_rate: 0.10
                    om_con: 0.3326     
                    om_annual: 0.075 #USD/kWh/year
        power_supply_G3:
            essentials:
                name: 'National Power Supply'
                color: '#C5ABE3'
                parent: supply
                carrier: electricity
            constraints:
                resource: inf
                lifetime: 40
            costs:
                monetary:
                    interest_rate: 0.10
                    om_con: 0.3195   
                    om_annual: 0.075 #USD/kWh/year                                
        
        PV:
            essentials:
                name: 'PV power plant'
                color: '#e6c643'
                parent: supply
                carrier_out: electricity
            constraints:
                energy_cap_max: 300 #net billing
                export_carrier: electricity
                resource: file=5kwh.csv:electricity
                resource_unit: energy_per_cap
                lifetime: 30 
                force_resource: true    
            costs:
                monetary:
                    interest_rate: 0.10
                    om_annual_investment_fraction: 0.1 #USD/kWh https://www.cne.cl/wp-content/uploads/2024/06/Informe-Final-Estudio-de-Costos-de-Inversion-2019.pdf
                    energy_cap: 771 # USD/kW https://www.cne.cl/wp-content/uploads/2024/06/ICTG-Mayo-2024.pdf
                    export: -0.0896 #USD/KWh https://www.cne.cl/wp-content/uploads/2024/05/Rex.-CNE-N257-2024-aprueba-ITP-PNP-2024-1.pdf
    
        battery:
            essentials:
                color: '#3B61E3'
                name: 'Battery'
                parent: storage
                carrier: electricity
            constraints:
                energy_eff: 1.0
                storage_cap_max: inf
                lifetime: 10
            costs:
                monetary:
                    interest_rate: 0.1
                    energy_cap: 288 #USD/kW https://energystorage.pnnl.gov/pdf/pnnl-28866.pdf
                    om_annual: 10 #USD/kW-year https://energystorage.pnnl.gov/pdf/pnnl-28866.pdf
                    storage_cap: 271  #USD/kWh https://energystorage.pnnl.gov/pdf/pnnl-28866.pdf

-----------------
     
Timeseries_data
--------

5kwh.csv
~~~~

+---------------------+-------------+
| Data                | electricity |
+=====================+=============+
| 2024-01-01 00:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 01:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 02:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 03:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 04:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 05:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 06:00:00 | 0           |
+---------------------+-------------+
| 2024-01-01 07:00:00 | 0.03        |
+---------------------+-------------+
| 2024-01-01 08:00:00 | 0.138       |
+---------------------+-------------+
| 2024-01-01 09:00:00 | 0.347       |
+---------------------+-------------+
| ...                 | ...         |
+---------------------+-------------+
| 2024-12-31 23:00:00 | 0           |
+---------------------+-------------+

demand_profiles.csv
~~~~

+---------------------+---------+----------+---------+-----+---------+
| Date                | 9900002 | 9900003  | 9900004 | ... | 9908546 |
+=====================+=========+==========+=========+=====+=========+
| 2024-01-01 00:00:00 | -31.075 | -93.84   | -29.02  | ... | -0.052  |
+---------------------+---------+----------+---------+-----+---------+
| 2024-01-01 01:00:00 | -28.725 | -94.19   | -19.54  | ... | -0.035  |
+---------------------+---------+----------+---------+-----+---------+
| 2024-01-01 02:00:00 | -22.825 | -105.92  | -19.62  | ... | -0.032  |
+---------------------+---------+----------+---------+-----+---------+
| 2024-01-01 03:00:00 | -23.175 | -101.84  | -19.62  | ... | -0.044  |
+---------------------+---------+----------+---------+-----+---------+
| ...                 | ...     | ...      | ...     | ... | ...     |
+---------------------+---------+----------+---------+-----+---------+
| 2024-12-31 23:00:00 | -25.136 | -182.069 | -8.924  | ... | -0.067  |
+---------------------+---------+----------+---------+-----+---------+

.. _model:

model.yaml
--------
.. code-block:: yaml

    import:  # Import other files from paths relative to this file, or absolute paths
        - 'model_config/techs.yaml'
        - 'model_config/locations.yaml'
        - 'scenarios_E1_G1.yaml'
        - 'scenarios_E1_G2.yaml'
        - 'scenarios_E1_G3.yaml'    
    model:
        name: Chilquinta model E1

        # What version of Calliope this model is intended for
        calliope_version: 0.6.8

        # Time series data path - can either be a path relative to this file, or an absolute path
        timeseries_data_path: 'timeseries_data'

        subset_time: ['2024-01-01', '2024-12-31']  # Subset of timesteps

    run:
        mode: plan  # Choices: plan, operate

        solver: gurobi

        ensure_feasibility: true # Switching on unmet demand

        bigM: 1e6 # setting the scale of unmet demand, which cannot be too high, otherwise the optimisation will not converge

        objective_options.cost_class: {monetary: 1}

scenarios_E1.yaml
--------
.. code-block:: yaml

    overrides:
        ID-E1:
            locations:
                demand:
                    techs:
                        power_demand:
                            constraints:
                                resource: file=demand_profiles.csv:ID
                        power_supply_G(group):
                        PV:
scenarios_E2.yaml
--------
.. code-block:: yaml

    overrides:
        ID-E2:
            locations:
                demand:
                    techs:
                        power_demand:
                            constraints:
                                resource: file=demand_profiles.csv:ID
                        PV:
                        battery:

scenarios_E3.yaml
--------
.. code-block:: yaml

    overrides:
        ID-E3:
            locations:
                demand:
                    techs:
                        power_demand:
                            constraints:
                                resource: file=demand_profiles.csv:ID
                        power_supply_G(group):
                        PV:
                        battery:

scenarios_E4.yaml
--------
.. code-block:: yaml

    overrides:
        ID-E3:
            locations:
                demand:
                    techs:
                        power_demand:
                            constraints:
                                resource: file=demand_profiles.csv:ID
                        power_supply_G(group):
                        PV:
                        battery:

scenarios_E5.yaml
--------
.. code-block:: yaml

    overrides:
        ID-E3:
            locations:
                demand:
                    techs:
                        power_demand:
                            constraints:
                                resource: file=demand_profiles_weekly.csv:ID
                        power_supply_G(group):
                        PV:
                        battery:    