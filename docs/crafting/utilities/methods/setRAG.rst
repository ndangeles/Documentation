setRAG
======

**When to use**
    
Use the setRAG method when you want to set an element color as Red, Ambar or Green according to the specified conditions. 

**Syntax**

.. sourcecode:: js

    setRAG(element: any, value: string, condition1: boolean, condition2: boolean, condition3: boolean, createContainer: boolean = true) 

**Example**

.. sourcecode:: js

    SW.setRAG(e, value, i.value>15, (i.value>=5 && i.value<15), i.value<5);
    
**Arguments**

Explaining the result from the template above:
    * When i.value is greater than 15 then the color of element **e** will be Red
    * When i.value is between 5 and 15 then the color of element **e** will be Ambar
    * When i.value is less than 5 then the element **e** will be Green 