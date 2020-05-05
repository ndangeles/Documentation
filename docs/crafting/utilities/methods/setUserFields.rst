setUserfields
=============

**When to use**

Use the setUserfields method when you want to update one or more documents with the same userfield values.
This method can also be used as a bulk action.

**Syntax**

.. sourcecode:: js

    setUserFields(documentType: string, documents: string[], documentUserFieldsValue: any[]); 

This method requires 3 parameters:
    * documentType: string
    * documents: string[]
    * documentUserFieldsValue: any[]);

**Example**

.. sourcecode:: js

    var documentUserFieldsValue = [
             {
                 "ColumnName": "Country",
                 "Value": "Portugal"
             },
             {
                 "ColumnName": "Currency",
                 "Value": "EUR"
             }
         ];
    
    SW.setUserFields('deliverable',['eaa68989-5726-4d65-83bb-0398b2abeda2', 'faa32152-2446-sdf1-vwet1-03sss2a42122'], documentUserFieldsValue);

**Arguments**

To have a better understanding on how to set the parameters, please see below:
    * documentType is the entity that will be updated: Project, Deliverable, Expense..
    * documents is an array of documentId that will be updated
    * documentUserFieldsValue is an array of userfields and corresponding value to be updated
    
