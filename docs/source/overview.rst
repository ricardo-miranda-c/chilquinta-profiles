Overview
=====

The next figure illustrates the methodology developed for this study,
breaking it down into the main components: **data filtering**, **defined parameters**, **analyzed scenarios**,
**main model**, and **results**. Each section plays a specific role in ensuring the quality,
consistency, and robustness of the final model.

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/Methodology.jpg
   :alt: Methodology
   :width: 800px
   :align: center

The **filtering section** is the initial and critical step, aimed at cleaning and validating
the raw data provided by the electricity distributor. This data consists of thousands of hourly demand profiles,
which must undergo a series of quality checks before being used in modeling.

This filtering process involves four key stages:

1. **Verification with the ID database**: The first stage cross-references the received profiles with an official ID database.
Only those profiles with a valid and verified match are retained, discarding any erroneous, duplicated, or unknown entries.

2. **Validation of complete profiles (8760 hours)**: Since the model works with hourly profiles over a full year
(365 days × 24 hours = 8760 hours), any profiles lacking complete data for the year are automatically discarded.
This criterion ensures consistency and allows for meaningful annual energy analysis.

3. **Allowance for minor data loss**: A maximum data loss of 24 hours (i.e., one day) is tolerated.
Profiles that are slightly incomplete, but miss no more than 24 hourly records and are otherwise consistent,
may still be included. This flexibility addresses minor measurement or transmission issues.

4. **Exclusion of zero-value profiles**: Finally, profiles that consist entirely of zeros throughout the year are removed.
Even if they meet the 8760-hour requirement, profiles with no variation or measurable demand are considered non-informative
or erroneous for the purposes of the analysis.

This rigorous process ensures that only high-quality and representative demand profiles are used in
subsequent stages of the study. Once the data is cleaned, the workflow proceeds to the definition of technical parameters,
formulation of energy scenarios, implementation of the optimization model, and evaluation of the results.

Categories
~~~~

The consumption profiles used in this study were provided by the electricity distribution company of the Valparaíso region,
which serves over 665,000 customers and is the fourth largest in Chile.

After filtering, only profiles with 8,760 hourly data points (a full year) were used. In total, **6,617 profiles** were analyzed.

For privacy reasons, the company did not include geographic coordinates—only the **category** and **subcategory** of each profile.
As a result, a standard location was assigned for all cases.

The profiles were grouped into **7 main categories** (Commercial, Fiscal, Industrial, Public Utility, Agriculture, Residential, and Municipal)
and **76 subcategories**.

The figure below shows a scatter plot of the profiles, with **annual energy consumption (kWh)** on the x-axis and **peak demand (kW)** on the y-axis
. A general trend can be seen: higher consumption usually implies higher demand. Most profiles are concentrated in the lower range of each category.

.. image:: C:/Users/rmiranda/Desktop/chilquinta-profiles/docs/img/categories_demand.jpg
   :alt: Methodology
   :width: 800px
   :align: center

This study classifies electricity demand profiles into three distinct groups based on the Chilean electricity market
regulation for *free customers*: **G1**, **G2**, and **G3**.

- **Group G1** includes profiles with a *monthly consumption of less than 350 kWh*,
referred to as *small consumption*. These users typically have lower energy demands and are subject to specific pricing schemes.
  
- **Group G2** consists of profiles with a *monthly consumption between 350 kWh and 500 kWh*,
categorized as *medium consumption*. These consumers have moderate electricity usage and fall under a transitional regulatory regime.

- **Group G3** represents profiles with a *monthly consumption greater than 500 kWh*,
which fall under the *stabilized price consumption* category. These are larger consumers who are more
exposed to the spot market and long-term contracts.

This categorization is essential for understanding how demand-side behavior varies across different customer segments
and how each group interacts with energy technologies and tariffs. 

The number of profiles within each group and their
respective characteristics are summarized below.

+-------+-----------+-------------+-------------+-----------+------------+----------------+--------+
| Group | Comercial | Agriculture | Residential | Municipal | Industrial | Public Utility | Fiscal |
+=======+===========+=============+=============+===========+============+================+========+
| G1    | 465       | 62          | 1043        | 26        | 25         | 16             | 13     |
+-------+-----------+-------------+-------------+-----------+------------+----------------+--------+
| G2    | 90        | 23          | 117         | 13        | 10         | 6              | 6      |
+-------+-----------+-------------+-------------+-----------+------------+----------------+--------+
| G3    | 2303      | 835         | 606         | 341       | 272        | 142            | 203    |
+-------+-----------+-------------+-------------+-----------+------------+----------------+--------+
