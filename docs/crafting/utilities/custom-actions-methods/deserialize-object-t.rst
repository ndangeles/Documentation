DeserializeObject<T>
====================

| Allows you to deserialize a JSON string, converting it to a type T.

.. code-block:: c#
    :linenos:

    T DeserializeObject<T>(string jsonString)


| Usage Example:

.. code-block:: c#
    :linenos:

    var deserializedObject = Host.dynamic DeserializeObject<CarDto>("'car': { 'model': 'Agera R', 'brand': 'koenigsegg'}");