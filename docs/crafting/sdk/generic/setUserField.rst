setUserfield
============

**When to use**

Use the setUserfield method when you want to update many userfield values on a single documents.

**Syntax**

.. sourcecode:: js

    setUserField(documentType: string, documentId: string, documentUserFieldsValue: any[]); 

This method requires 3 parameters:
    * documentType: string
    * documentId: string
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
    
    SW.setUserField('deliverable','eaa68989-5726-4d65-83bb-0398b2abeda2', documentUserFieldsValue);

**Arguments**

To have a better understanding on how to set the parameters, please see below:
    * documentType is the entity that will be updated: Project, Deliverable, Expense..
    * documentId is the documentId that will be updated
    * documentUserFieldsValue is an array of userfields and its corresponding value to be updated
    
