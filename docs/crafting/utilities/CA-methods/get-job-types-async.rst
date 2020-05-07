GetJobTypesAsync
================

| Get a list of Job Types asynchronously.

.. code-block:: c#
    :linenos:

    Task<IEnumerable<IJobTypeObject>> GetJobTypesAsync(string filterName = "all", string name = "", Guid? clientId = null,
            Guid? departmentId = null, IEnumerable<Guid> departments = null, int skip = 0, int take = 0,
            string documentTypeName = "", Guid? businessObjectTypeId = null, Guid? parentJobTypeId = null)

| Usage Example:

.. code-block:: c#
    :linenos:

    var jobTypesList = await Host.GetJobTypesAsync("all", "", "AE449D34-81B9-4BAF-AF8C-0F434D42726D", 
        "F843C2C5-7449-40D9-8D84-01CF5E2A9D06", null, 0, 100, "", null, null);