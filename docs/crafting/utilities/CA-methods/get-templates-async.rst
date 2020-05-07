GetTemplatesAsync
=================

| Get a list of Templates asynchronously.

.. code-block:: c#
    :linenos:

    Task<IEnumerable<TemplateDto>> GetTemplatesAsync(int skip, int take, string type = null, 
            string name = null, string documentId = null, string documentTypeName = null)

| Usage Example:

.. code-block:: c#
    :linenos:

    var templatesList = await Host.GetTemplatesAsync(0, 100, ""CreateSubEstimatesFromProjectDisciplines"", 
        null, "AE449D34-81B9-4BAF-AF8C-0F434D42726D", null)