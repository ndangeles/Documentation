GetJobTypeByIdAsync
===================

| Gets a Job Type by ID asynchronously.

.. code-block:: c#
    :linenos:

    Task<IJobTypeObject> GetJobTypeByIdAsync(Guid id)


| Usage Example:

.. code-block:: c#
    :linenos:

    var jobType = await Host.GetJobTypeByIdAsync("AE449D34-81B9-4BAF-AF8C-0F437D42726D");