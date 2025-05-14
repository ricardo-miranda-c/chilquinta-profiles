Scenarios
=========

Scenario 1: PV only
----------
Scenario E1 presents a somewhat unconventional configuration. It assumes that the existing grid
connection supplies electricity to meet demand, while a photovoltaic (PV) plant operates in parallel,
providing electricity according to its generation profile—without any associated energy storage system.

This setup allows for the analysis of how different demand profiles choose to prioritize energy
usage from either the grid or the PV plant, depending on associated costs and system characteristics.

It is important to highlight that the PV plant is capped at a maximum installed capacity of 300 kW,
as previously mentioned, whereas the grid connection is unrestricted—ensuring that there is no risk of unmet demand.
Additionally, the PV system is allowed to sell surplus energy back to the grid,
enhancing its overall performance and economic viability.

.. image:: docs/img/E1.jpg
   :alt: Battery distribution
   :width: 400px
   :align: center

Scenario 2: PV + battery
----------
This scenario, which involves the installation of a photovoltaic (PV) plant
paired with a dedicated storage system—specifically, a battery. This setup represents an islanded system,
meaning it operates independently from the electrical grid.

The PV plant is capable of supplying electricity directly to meet demand when solar generation aligns with consumption.
In periods of excess generation, surplus energy can be stored in the battery for later use.
The storage capacity is determined by the level of overproduction, allowing the system to adapt to different generation profiles.

However, because there is no grid connection to cover shortfalls, unmet demand may occur, depending on the variability
and shape of the load profile.

.. image:: docs/img/E2.jpg
   :alt: Battery distribution
   :width: 400px
   :align: center

Scenario 3: PV + battery + grid connection
----------
Scenario E3, illustrated in Figure 6, represents a more realistic and widely applicable configuration. It combines the elements of
Scenario E2—a photovoltaic (PV) system with battery storage—with an active grid connection.

The main advantage of this setup over the previous scenario lies in its ability to fully meet the electricity demand,
as the grid serves as a reliable backup. At the same time, the PV system and battery can be leveraged to reduce overall
energy costs by prioritizing self-generation and storage. Additionally, any surplus energy can be exported to the grid,
improving the system's economic performance.

As with previous scenarios, the decision on the optimal installed capacity—whether from the PV plant or the grid—depends
on each profile's load characteristics, such as peak demand and consumption behavior.

.. image:: docs/img/E3.jpg
   :alt: Battery distribution
   :width: 400px
   :align: center

Scenario 4: PV + battery + grid connection + clustering.
----------

The scenario E4 it has the same layout as scenario E3, but in this case,
the demand is subjected to a Calliope native clustering operation. The main function of this application is to improve
the energy optimization of systems where specifically there is seasonal storage and complex temporal dynamics.
This formulation and objective function is described in :doc:`clustering`

.. image:: docs/img/E4.jpg
   :alt: Battery distribution
   :width: 400px
   :align: center

Scenario 5
----------
The modification of this scenario aims to analyze the behavior of both demand and model outputs when
a randomly selected week from each demand profile is duplicated to replace all other weeks throughout the year.
To achieve this, a custom script was developed to randomly select a week from each profile and generate new
profiles with the same ID, which can then be compared with the original profiles.
This formulation is described in :doc:`demand_analysis`.

.. image:: docs/img/E5.jpg
   :alt: Battery distribution
   :width: 400px
   :align: center