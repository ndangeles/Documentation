Custom Action Methods
=====================

**Host keyword**

| The Host keyword allows the user to access the available functions.
| For more information, you can access each function documentation for more informations.

.. code-block:: c#
    :linenos:

    Host.DeleteEstimateItems(estimate);



**CurrentUser keyword**

| The CurrentUser is available for one to access the currently logged user and its properties.

.. code-block:: c#
    :linenos:

    var userName = CurrentUser.UserName;



**Document keyword**

| The Document object represents the business object where the workflow transition was triggered.
| For one to access its properties, a cast needs to be made. In the following example, the user knows the action will be added to an Estimate workflow stage transition.

.. code-block:: c#
    :linenos:

    var estimate = Document as IEstimateObject estimate;



| Below are described the available C# functions to be used when creating a new custom action.

.. toctree::
   :glob:
   
   *