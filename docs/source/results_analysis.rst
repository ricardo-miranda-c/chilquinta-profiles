Results Analysis
================

Key Metrics
-----------

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

Where:
- \( y \): Year of operation.
- \( x \): Power plant or generation unit.
- \( t \): Time interval.
- \( \text{cost}(y,x) \): Total cost for unit \( x \) in year \( y \).
- \( e_{\text{cap}}(y,x) \): Capacity of unit \( x \) in year \( y \).
- \( e_{\text{prod}}(y,x,t) \): Energy produced by unit \( x \) in year \( y \) and time \( t \).

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

Where:
- \( y \): Year of operation.
- \( x \): Power plant or generation unit.
- \( t \): Time interval.
- \( e_{\text{prod}}(y,x,t) \): Energy produced by unit \( x \) in year \( y \) and time \( t \).
- \( e_{\text{cap}}(y,x) \): Capacity of unit \( x \) in year \( y \).
- \( \text{timeres}(t) \): Time resolution or duration of interval \( t \).
