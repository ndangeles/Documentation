CreateJobsFromEstimateDeliverableQuantity
=========================================

**Compatible documents**
Estimate

**When to use**

| This action will create a Job for each Estimate Item (Deliverable) x Quantity.
| (Remember: This code is the default implementation which can be modified anytime in the system)

.. code-block:: c#
    :linenos:

    var estimate = Document as IEstimateObject;
    foreach (var deliverable in estimate.EstimateItemObjects)
    {
        for (int i = 0; i < deliverable.QuantityIncome; i++)
        {
            var newJob = Host.CreateJob();
            newJob.CompanyObject = estimate.CompanyObject;
            newJob.ClientObject = estimate?.JobObject?.ClientObject ?? (estimate?.ProjectObject?.ClientObject ?? estimate?.ClientObject);
            newJob.ProjectObject = estimate.ProjectObject;
            newJob.ProductObject = estimate?.JobObject?.ProductObject ?? (estimate?.ProjectObject?.CommercialClientProductObject ?? estimate?.ProductObject);
            newJob.Subject = deliverable.Name + " - " + (i+1);
            newJob.DepartmentObject = estimate?.JobObject?.DepartmentObject ?? estimate?.ProjectObject?.DepartmentObject;
                newJob.JobTypeObject = estimate?.JobObject?.JobTypeObject ?? estimate?.JobTypeObject;
                newJob.EntryDateUtc = estimate?.JobObject?.EntryDateUtc ?? (estimate?.ProjectObject?.BeginDate ?? estimate.Date);
                newJob.EntryDateLocal = estimate?.JobObject?.EntryDateLocal ?? (estimate?.ProjectObject?.BeginDate ?? estimate.Date);
                newJob.EstimatedDateLocal = estimate?.JobObject?.EstimatedDateLocal ?? (estimate?.ProjectObject?.EndDate ?? estimate.Expiration);
                newJob.EstimatedDateUtc = estimate?.JobObject?.EstimatedDateUtc ?? (estimate?.ProjectObject?.EndDate.FromSkillsTimeToUtc() ?? estimate.Expiration.FromSkillsTimeToUtc());
                newJob.RequestedDateLocal = estimate?.JobObject?.RequestedDateLocal ?? estimate?.ProjectObject?.EndDate.AddHours(1) ?? estimate.Expiration.AddHours(1);
                newJob.RequestedDateUtc = estimate?.JobObject?.RequestedDateUtc ?? estimate?.ProjectObject?.EndDate.AddHours(1).FromSkillsTimeToUtc() ?? estimate.Expiration.AddHours(1).FromSkillsTimeToUtc();
                newJob.AgreedDateLocal = estimate?.JobObject?.AgreedDateLocal ?? estimate?.ProjectObject?.EndDate.AddHours(1) ?? estimate.Expiration.AddHours(1);
                newJob.AgreedDateUtc = estimate?.JobObject?.AgreedDateUtc ?? estimate?.ProjectObject?.EndDate.AddHours(1).FromSkillsTimeToUtc() ?? estimate.Expiration.AddHours(1).FromSkillsTimeToUtc();
                newJob.ParentJobObject = estimate?.JobObject;
            }
        }