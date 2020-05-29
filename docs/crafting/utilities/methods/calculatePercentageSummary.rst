calculatePercentageSummary
++++++++++++++++++++++++++

**When to use**

Use the calculatePercentageSummary method when you want calculate a percentage summary in a data grid.

**Syntax**

.. sourcecode:: js

    calculatePercentageSummary(options: any, dividend: string[], divisor: string[])

**Example**

.. sourcecode:: js

    SW.calculatePercentageSummary(options, ['BillableTime', 'ForecastTime'], ['Capacity']);
    
**Arguments**

Explaining the result from the method above:
    * (BillableTime + ForecastTime) / Capacity
