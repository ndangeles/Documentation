GetDepartmentByIdAsync
======================

| Gets a Department by ID asynchronously.

.. code-block:: c#
    :linenos:

    Task<IDepartmentObject> GetDepartmentByIdAsync(Guid departmentId)


| Usage Example:

.. code-block:: c#
    :linenos:

    var department = await Host.GetDepartmentByIdAsync("AE449D34-81B9-4BAF-AF8C-0F437D42726D");