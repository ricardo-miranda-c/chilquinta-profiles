Results
=======

Battery
~~~~

This section analyzes storage use across user groups, scenarios, and years.
**Scenario E1** is excluded since it does not include storage.

In **groups G1 and G2** for **2024**, scenarios **E3, E4, and E5** show a similar pattern:
most profiles have a **battery capacity <1 kW** and a **utilization factor between 30–45%**.
Scenario **E5** shows slightly higher utilization (up to 48%), likely due to more stable demand profiles.

For **group G3**, most profiles have battery capacities under **40 kW** and utilization between **35–45%**.
However, many profiles display a **negative correlation** — as battery capacity increases, utilization decreases,
in some cases down to **20%**. The profile distribution in scenarios E3, E4, and E5 for G3 forms a cone shape,
each bounded by scenario-specific limits.

**Scenario E2**, although grid-independent and unchanged between years, reveals two clear patterns:
- Some profiles have **larger battery capacities** with **very low utilization (0–5%)**
- Others show **small battery capacities (<3 kW)** but **high utilization**

A portion of profiles in E2 shows a **positive correlation** between capacity and usage.
For **group G3 in scenario E1**, most data is concentrated below **400 kW of battery capacity**,
with battery utilization varying from **0 to 40%**.

.. note::

    - **X-axis**: Battery installed capacity  
    - **Y-axis**: Battery utilization factor  
    - **Bubble size**: Peak demand  
    - **Color**: LCOE (Levelized Cost of Energy)

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/Battery.jpg
   :alt: Methodology
   :width: 800px
   :align: center

Supply
~~~~

This section analyzes the effect of the power grid on each user group. Figure below presents a scatter plot where:

.. note::

    - **X-axis**: Grid installed capacity  
    - **Y-axis**: Grid utilization factor  
    - **Bubble size**: Peak demand  
    - **Color**: LCOE (Levelized Cost of Energy)

**Scenario E2** is excluded since it lacks grid connection.

For **G1 and G2**, grid capacity is usually under 20 kW and utilization is low (<10%), indicating a higher reliance on PV and batteries.
For **G3**, grid capacity often exceeds 1000 kW, and utilization reaches up to 70%, showing strong grid dependence due to higher demand
and the 300 kW PV limit.

LCOE values vary notably:
- **G1 and G2**: LCOE around -0.046 USD/kWh due to lower grid costs and higher PV self-generation with surplus sales.
- **G3**: LCOE around 0.05 USD/kWh due to higher grid costs and limited PV contribution.

The color scale in the plot was adjusted to improve interpretation by excluding extreme LCOE values.

Scenario differences are noticeable. In **E1**, profiles with low grid use and demand show lower LCOE, while those with greater reliance
on the grid show higher costs. Some exceptions with low capacity but high usage show inconsistencies, suggesting more complex behaviors
in certain profiles.

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/Supply.jpg
   :alt: Methodology
   :width: 800px
   :align: center

Demand sensibility analysis
~~~~

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/2024_2025_lcoe_dist.jpg
   :alt: Methodology
   :width: 800px
   :align: center

LCOE analysis  
~~~~

This section analyzes how much variation exists between scenarios in terms of **Levelized Cost of Energy (LCOE)**.
A **Games-Howell statistical test** was applied to compare the LCOE values by group and year, using **violin plots**
to visualize the distribution.

At first glance, the plots for both years appear almost identical, though they differ slightly.
**Scenario E2 for group G3** was separated due to its high deviation, which made the main graph unclear.

.. note::

    Key findings:

    - In **groups G1 and G2**, the **average LCOE is negative** in all scenarios.
    - In **group G3**, the average LCOE is **positive**, mainly due to **18% of profiles** with extremely high values (up to **25 USD/kWh**).
    - For **group G1**, scenarios **E1, E3, and E5** show a similar distribution, with most values around **-0.05 USD/kWh**.
    - Scenario **E2** has some upward deviation, reaching around **-0.037 USD/kWh**.
    - Scenario **E4** shows slightly lower results than others.
    - In **group G3**, after separating E2, the remaining scenarios show an average near **-0.02 USD/kWh**.
    - In E2 for G3, **81.7%** of profiles have **negative LCOE**, while **18.3%** are **positive**.

This analysis helps to understand the economic behavior of different scenarios across consumption groups.

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/LCOE_analysis.jpg
   :alt: Methodology
   :width: 800px
   :align: center