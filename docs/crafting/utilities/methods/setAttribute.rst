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