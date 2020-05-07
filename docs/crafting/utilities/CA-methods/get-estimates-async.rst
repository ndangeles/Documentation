GetEstimatesAsync
=================

| Get a list of Estimates asynchronously.

.. code-block:: c#
    :linenos:

    Task<IEnumerable<IEstimateObject>> GetEstimatesAsync(int skip = 0, int take = 0, string filter = null, 
        Guid? clientId = null, Guid? projectId = null, Guid? deliverableId = null, Guid? contractId = null, Guid? parentId = null)


| Usage Example:

.. code-block:: c#
    :linenos:

    var estimatesList = await Host.GetEstimatesAsync(0, 100, null, "AE449D34-81B9-4BAF-AF8C-0F434D42726D", 
        "F843C2C5-7449-40D9-8D84-01CF5E2A9D06", null, null, null);