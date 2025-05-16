Model Parameters
================

This section describes the parameters used in the model, including the constraints and costs for
photovoltaic plants and batteries, as well as the simulation parameters for PV panels. Additionally,
it provides information on the costs associated with electricity consumer groups in Chile for the years
2024 and 2025.
The parameters are essential for understanding the model's behavior and performance, as they define
the characteristics of the energy system being analyzed.


The model considers various constraints and costs associated with photovoltaic plants and batteries.
These parameters are crucial for determining the feasibility and economic viability of the energy
system being analyzed. The following table summarizes the key constraints and costs for each technology:

Constraints and costs for photovoltaic plants and battery
~~~~

The following table summarizes the constraints and costs associated with photovoltaic plants and batteries
used in the model. These parameters are essential for understanding the performance and economic
viability of the energy system being analyzed.

+-----------+---------------------+----------------+------------------+-------------------+--------------------------+---------------------------+-----------------------+------------------+
| Equipment | Energy cap max (kW) | Efficiency (%) | Lifetime (years) | Interest rate (%) | Energy capacity (USD/kW) | O&M annual (Usd/kWh/year) | Storage cap (USD/kWh) | Export (USD/kWh) |
+===========+=====================+================+==================+===================+==========================+===========================+=======================+==================+
| PV        | 300                 | -              | 30               | 10                | 771                      | 7.71                      | -                     | -0.0896          |
+-----------+---------------------+----------------+------------------+-------------------+--------------------------+---------------------------+-----------------------+------------------+
| Battery   | -                   | 100            | 15               | 10                | 288                      | 10                        | 270                   | -                |
+-----------+---------------------+----------------+------------------+-------------------+--------------------------+---------------------------+-----------------------+------------------+

----------------------

PV panels simulation parameters
~~~~

The following table summarizes the simulation parameters for the photovoltaic panels used in the model.

+-------------+----------+-------------+
| Parameters  | Value    | Unit        |
+=============+==========+=============+
| Lon         | -68.8685 | °           |
+-------------+----------+-------------+
| Lat         | -23.5226 | °           |
+-------------+----------+-------------+
| Capacity    | 1        | kW          |
+-------------+----------+-------------+
| System loss | 10       | %           |
+-------------+----------+-------------+
| Tilt        | 35       | °           |
+-------------+----------+-------------+
| Azimuth     | 180      | °           |
+-------------+----------+-------------+
| Radiation   | 5        | (kW/m2)/day |
+-------------+----------+-------------+
| Tracking    | None     | -           |
+-------------+----------+-------------+
| Dataset     | Merra2   | -           |
+-------------+----------+-------------+


The following figure illustrates the photovoltaic behavior of the system, showing the energy production
over time. The data used for this simulation is based on the Merra2 dataset, which provides
information on solar radiation and other relevant parameters. The figure displays the energy production
of the photovoltaic panels over a specific period, allowing for an analysis of the system's performance
and efficiency. The parameters used in the simulation, such as tilt, azimuth, and system loss,
are essential for accurately modeling the energy production of the photovoltaic panels.

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/PV_2024.jpg
   :alt: Photovoltaic behavior
   :width: 600px
   :align: center

----------------------

Costs referred to the electricity consumer groups (G1, G2 and G3) in Chile for the years 2024 and 2025.
~~~~

The following table summarizes the costs associated with electricity consumer groups in Chile for
the years 2024 and 2025.

+------+----------------------------+------------------+---------------------------+
| year | Tariff | Interest rate (%) | O&M con (USD/kW) | O&M annual (USD/kWh/year) |
+======+========+===================+==================+===========================+
| 2024 | G1     | 10                | 0.2419           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+
| 2024 | G2     | 10                | 0.2428           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+
| 2024 | G3     | 10                | 0.2439           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+
| 2025 | G1     | 10                | 0.3531           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+
| 2025 | G2     | 10                | 0.3326           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+
| 2025 | G3     | 10                | 0.3195           | 0.075                     |
+------+--------+-------------------+------------------+---------------------------+

----------------------

.. _optimization-objective:

Optimization objective option
~~~~

Formaly, the main goal of the model is to minimize the costs of the energy system to cover the
energy demand given a set of different technologies and scenarios.
Next ecuation, presents the optimization objective with technology represented by :math:`y`,
location by :math:`x`, and cost class by :math:`k`

.. math::

   \min \left[ \sum_x \left( \text{cost}_{\text{con}}(x, k) + \sum_x \text{cost}_{\text{op}}(x, k) \right) \right]

The optimization focusses on minimizing the overall systems costs associated with each technology to
cover the demand in each timestep. The objective function calculates the annual system costs,
which is the sum of construction costs (:math:`\text{cost}_{\text{con}}`) and operation and maintenance costs (:math:`\text{cost}_{\text{op}}`).
The construction costs are calculated using the depreciation rate (:math:`d(y,k)`), demand time series (:math:`\text{timeseries}(t)`),
storage costs (:math:`\text{cost}_{s\_cap}`), installed storage capacity (:math:`s_\text{cap}`),
installed energy capacity costs (:math:`\text{cost}_{e\_cap}`), and installed energy capacity (:math:`e_\text{cap}`).

.. math::

   \text{cost}_{\text{con}}(y, x, k) = d(y, k) \cdot \left( \frac{\sum_t \text{timeres}(t)}{8760} \right)\cdot
   
   
    \sum \left[ \text{cost}_{s\_cap}(y, k) \cdot s\_cap(y, x) + \text{cost}_{e\_cap}(y, k) \cdot e\_cap(y, x) \right]

The depreciation rate (:math:`d(y,k)`) is defined in the next ecuation. Where :math:`i` represents the interest rate. 

.. math::

   d(y, k) = \frac{i \cdot \left(1 + i(y, k)\right)^{\text{plantlife}(k)}}{\left(1 + i(y, k)\right)^{\text{plantlife}(k)} - 1}

The operating and maintenance costs (O&M) of the model, as defined in the next equation,
include fixed costs (:math:`\text{cost}_{\text{op, fixed}}`) which depend on the installed capacity of the equipment,
variable costs (:math:`\text{cost}_{\text{op, var}}`) determined by the estimated production of the equipment,
and fuel costs (:math:`\text{cost}_{\text{op, fuel}}`) directly associated with the fuel used.

.. math::

   \text{cost}_{\text{op}}(y, x, k) = \text{cost}_{\text{op, fixed}}(y, x, k) + \text{cost}_{\text{op, var}}(y, x, k) + \text{cost}_{\text{op, fuel}}(y, x, k)

The variable operation and maintenance costs presented in the next equation
further depend on the variable costs per unit (:math:`\text{cost}_{\text{om_var}}`) for each technology :math:`y` and cost class :math:`k`.

.. math::

   \text{cost}_{\text{op, var}}(y, x, k) = \text{cost}_{\text{om_var}}(y, k) \cdot \sum_t e_{\text{prod}}(y, x, t)

The storage capacities (:math:`s_\text{cap}`) considered in the modeling should not exceed the maximum storage capacity
(:math:`s_{\text{cap, max}}`) for each location, as shown in the next equation.

.. math::

   s_{\text{cap}}(y, x) \leq s_{\text{cap, max}}(y, x)

Likewise, each technology's energy capacity (:math:`e_\text{cap}`) should not exceed the maximum energy capacity (:math:`e_{\text{cap, max}}`)
available for each location.

.. math::

   e_{\text{cap}}(y, x) \leq e_{\text{cap, max}}(y, x)         

Regardless of the demands considered, they must be met based on the production (:math:`e_\text{prod}`),
consumption (:math:`e_\text{con}`), and export (:math:`e_\text{ex}`) of energy, as shown in the next equation.

.. math::

   \sum_z e_{\text{prod}}(y, x, t) + e_{\text{con}}(y, x, t) + e_{\text{ex}}(y, x, t) = 0  

The demand for each technology at each location is determined by the next ecuation,
where :math:`timeres(t)` represents the time-series with :math:`η` being the efficiency for each technology.

.. math::

   e_{\text{con}}(y, x, t) \cdot \eta(y, x, t) = \text{timeres}(t)   
----------