getEmptyGuidValue
+++++++++++++++++

**When to use**

Use the getEmptyGuidValue method when you want to set a value to a empty guid.

**Syntax**

.. sourcecode:: js

    getEmptyGuidValue(key: string, callback: Function) 

**Example**

.. sourcecode:: js

    SW.getEmptyGuidValue(key, () => SW.executeAPI('GET', `divisions/${key}/lookup`, null, {}));
