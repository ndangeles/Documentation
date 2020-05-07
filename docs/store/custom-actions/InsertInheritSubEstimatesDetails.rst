InsertInheritSubEstimatesDetails
================================

**Compatible documents**
Estimate

**When to use**

| This action will delete the Estimate Items (and Details) from the Estimate and after that it will recreate them with the most recent data from the Sub-Estimates.
| (Remember: This code is the default implementation which can be modified anytime in the system)

.. code-block:: c#
    :linenos:

    if (!(Document is IEstimateObject estimate) || estimate.ProjectObject == null) return ActionResult.Success();
    var subEstimates = await Host.GetEstimatesAsync(0, 100, null, null, null, null, null, estimate.Oid);
    Host.DeleteEstimateItems(estimate);
    foreach (var estimateItem in subEstimates.SelectMany(e => e.EstimateItemObjects))
    {
        estimateItem.CreateCopy(estimate);
    }
    return ActionResult.Success();