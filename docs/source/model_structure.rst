Model Structure
===============


- 2024
  - E1
    - model_config
      - locations.yaml
      - techs.yaml
    - timeseries_data
      - 5kwh_2024.csv
      - timeseries.csv
    - scenarios_E1_G1
    - scenarios_E1_G2
    - scenarios_E1_G3
  - E2
  - E3
  - E4
  - E5
- 2025
  
model_config
--------

locations.yaml
~~~~

.. note::

    locations:
        demand:
            coordinates: {lat: 40, lon: 20}

------------

techs.yaml
~~~~

.. note::

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
~~~~                

5kwh

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

-----------------

Demand profiles

+---------------------+---------+---------+---------+-----+
| Data                | 9900002 | 9900003 | 9900004 | ... |
+=====================+=========+=========+=========+=====+
| 2024-01-01 00:00:00 | -31.075 | -93.84  | -29.02  | ... |
+---------------------+---------+---------+---------+-----+
| 2024-01-01 01:00:00 | -28.725 | -94.19  | -19.54  | ... |
+---------------------+---------+---------+---------+-----+
| 2024-01-01 02:00:00 | -22.825 | -105.92 | -19.62  | ... |
+---------------------+---------+---------+---------+-----+
| 2024-01-01 03:00:00 | -23.175 | -101.84 | -19.62  | ... |
+---------------------+---------+---------+---------+-----+
| ...                 | ...     | ...     | ...     | ... |
+---------------------+---------+---------+---------+-----+

-----------------