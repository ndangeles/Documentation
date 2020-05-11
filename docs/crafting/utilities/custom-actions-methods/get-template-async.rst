GetTemplateAsync
================

| Gets a Template by ID asynchronously.

.. code-block:: c#
    :linenos:

    Task<TemplateDto> GetTemplateAsync(Guid id)


| Usage Example:

.. code-block:: c#
    :linenos:

    var template = await Host.GetTemplateAsync("AE449D34-81B9-4BAF-AF8C-0F437D42726D");