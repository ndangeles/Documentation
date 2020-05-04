
getUserFields
=============

**When to use**

Use the getUserfields method when you want to get the values of a specific userfield from one to several documents.

**Syntax**

.. sourcecode:: js

    getUserFields(documentType: string, documents: string[], userFieldName: string, valueType: string);

This method requires 4 parameters:
    * documentType: string
    * documents: string[]
    * userFieldName: string;
    * valueType: int

**Example**

.. sourcecode:: js

    SW.getUserFields('deliverable',['eaa68989-5726-4d65-83bb-0398b2abeda2','30ba442b-9159-45ee-a13a-abe5e665db3a'],'Currency', 5);

**Arguments**

To have a better understanding on how to set the parameters, please see below:
    * documentType is the entity that will be updated: Project, Deliverable, Expense..
    * documents is an array of documentId from which you want to obtain the values
    * userFieldName is the name of the userfield
    * valueType is the userfield type in the Integer format
        * Boolean = 0
        * Date = 1
        * Float = 2
        * Integer = 2
        * Money = 4
        * Varchar50 = 5
        * Varchar100 = 6
        * VarcharMax = 7
        * Text = 8
        * UniqueIdentifier = 9
    

