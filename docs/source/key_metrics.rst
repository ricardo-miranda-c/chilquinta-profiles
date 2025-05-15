Key Metrics
================

This section provides an overview of the key metrics used in the project to evaluate the performance and cost-effectiveness
of the energy systems. These metrics include the Levelized Cost of Energy (LCOE), Capacity Factor, and other relevant indicators.
These metrics are essential for understanding the economic viability of different energy generation technologies and
configurations, as well as for comparing the performance of different scenarios.

LCOE
~~~~
The Levelized Cost of Energy (LCOE) is a measure of the average cost of producing energy over the lifetime of a power plant.
It is calculated by dividing the total lifetime costs of the plant (including capital, operating, and maintenance costs)
by the total energy produced over its lifetime. The LCOE is expressed in terms of currency per unit of energy (e.g., USD/kWh)
and is a key metric for comparing the cost-effectiveness of different energy generation technologies.

The LCOE is calculated using the following formula:

.. math::

   LCOE = \frac{\sum_{y,x} \text{cost}(y,x)}{
   \sum_{y,x} e_{\text{cap}}(y,x) \cdot \sum_t e_{\text{prod}}(y,x,t)
   }

.. note::
   The project includes the following features:
    - :math:`y` : Technologies.
    - :math:`x` : Locations.
    - :math:`t` : Time interval.
    - :math:`cost(y,x)`  : Total cost for technologies :math:`x` in locations :math:`y`.
    - :math:`e_{\text{cap}}(y,x)`  : Capacity of technologies :math:`x` in locations :math:`y`.
    - :math:`e_{\text{prod}}(y,x,t)`  : Energy produced by technologies :math:`x` in locations :math:`y` and time :math:`t`.

Capacity Factor
~~~~~~~~~~~~~~~~
The capacity factor is a measure of how much energy a power plant produces compared to its maximum potential output.
It is calculated as the ratio of the actual output of the plant to the maximum possible output over a given period of time.
The capacity factor is expressed as a percentage and is an important metric for evaluating the performance of power plants,
especially renewable energy sources like wind and solar.

The capacity factor is influenced by several factors, including the availability of the energy source 
(e.g., sunlight for solar plants or wind for wind farms), the design and efficiency of the power plant,
and the operational strategy employed. A higher capacity factor indicates that a power plant is producing
energy more consistently and efficiently, while a lower capacity factor suggests that the plant is not operating
at its full potential.

The capacity factor is calculated using the following formula:

.. math::

   CF = \frac{\sum_{y,x,t} e_{\text{prod}}(y,x,t)}{
   \sum_{y,x} e_{\text{cap}}(y,x) \cdot \sum_t \text{timeres}(t)
   }

.. note::
   The project includes the following features:
    - :math:`y` : Technologies.
    - :math:`x` : Locations.
    - :math:`t` : Time interval.
    - :math:`e_{\text{prod}}(y,x,t)` : Energy produced by technologies :math:`x` in locations :math:`y` and time :math:`t`.
    - :math:`e_{\text{cap}}(y,x)` : Capacity of technologies :math:`x` in locations :math:`y`.
    - :math:`timeres(t)` : Time resolution or duration of interval :math:`t`.

Variation of the average percentage change (VAPC)
~~~~~~~~~~~~~~~~
The variation of the average percentage change (VAPC) is a metric used to evaluate the impact of demand modifications on the
average demand profile. It is calculated as the percentage change in the average demand before and after the modification.
The VAPC is expressed as a percentage and provides insight into how much the demand profile has changed due to the modification.

The VAPC is calculated using the following formula:

.. math::

   \Delta_\% = \frac{1}{N} \sum_{i=1}^N \frac{\left( \text{LCOE}_{E5, \text{ID}_i} \mp \text{LCOE}_{E3, \text{ID}_i} \right)}{\left| \text{LCOE}_{E3, \text{ID}_i} \right|} \cdot 100
