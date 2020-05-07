DeserializeObject
=================

| Allows you to deserialize a JSON string, converting it to a dynamic type object.

.. code-block:: c#
    :linenos:

    dynamic DeserializeObject(string jsonString)


| Usage Example:

.. code-block:: c#
    :linenos:

    var deserializedObject = Host.dynamic DeserializeObject("'car': { 'model': 'Agera R', 'brand': 'koenigsegg'}");