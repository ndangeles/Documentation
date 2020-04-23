SDK
===

There was a need to have a set of tools to be used on the system.
This SDK can be used anywhere on the system, but it is mostly used on Workspaces.

 .. note::

    Whenever you need to use any SDK method you will need to access to the namespace **SW**
     
     .. sourcecode:: js

        SW.methodName()

Methods
-------
Below you can find the methods available.

setAttribute
++++++++++++

    **When to use**

    Use the setAttribute method when you want to set a Class, Style or any other 
    attribute to an element. 

    **Syntax**

    .. sourcecode:: js

        setAttribute(element: any, text: string, attribute: string = "", attributeValue: string = "", createContainer: boolean = true) 

    **Example**

    .. sourcecode:: js

        SW.setAttribute(e, null,'style', 'display: flex; align-items: baseline', false)
        SW.setAttribute(e, 'Hello', 'style', 'background-color:red; color:white', true)
        SW.setAttribute(e, null, 'class', 'skillsSquare', false)

setRAG
++++++

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

