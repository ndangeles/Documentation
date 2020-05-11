GetDepartmentsAsync
===================

| Get a list of Estimates asynchronously.

.. code-block:: c#
    :linenos:

    Task<IEnumerable<IDepartmentObject>> GetDepartmentsAsync(string name = "", 
        Guid? companyId = null, Guid? divisionId = null, Guid? projectId = null, int skip = 0, int take = 0)


| Usage Example:

.. code-block:: c#
    :linenos:

    var departmentsList = await Host.GetDepartmentsAsync("Art", "912C8778-B437-46C7-B98D-2248E5E118A4", null, null, 0, 100);