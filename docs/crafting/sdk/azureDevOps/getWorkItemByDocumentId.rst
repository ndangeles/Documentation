getWorkItemByDocumentId
=======================

**When to use**

Use the getWorkItemByDocumentId method when you want to get the Work Item's data from Azure DevOps.

**Syntax**

.. sourcecode:: js

    getWorkItemByDocumentId(documentOid: string, documentTypeName: string, columnName: string, valueType: string, authorization: string, showError = true, organization: string , project: string ):

This method requires 3 parameters:
   * documentOid: string
   * documentTypeName: string
   * columnName: any
   * valueType: int
   * authorization: string
   * showError: boolean
   * organization: string
   * project: string

**Arguments**

To have a better understanding on how to set the parameters, please see below:
   * documentTypeName  is the entity that will be updated: Project, Deliverable, Expense..
   * documentOid is the Oid of the document to be updated
   * columnName is the userfield name where the work item id is field for the document
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
   * authorization is the Azure DevOps Basic authentication
   * showError identifies if in case of an error occurs, a toast should be shown with the error. By default is true 
   * organization is the organization name in Azure DevOps
   * project is the project name in Azure DevOps
    