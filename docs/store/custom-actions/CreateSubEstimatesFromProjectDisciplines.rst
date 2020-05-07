CreateSubEstimatesFromProjectDisciplines
========================================

**Compatible documents**
Estimate

**When to use**

| For each Department in the Estimate's Project, a new Estimate will be automatically created.
| If a template is available (which is not required), one can define per Job Type, the eligible Departments for the Estimate creation. 
| (Remember: This code is the default implementation which can be modified anytime in the system)

.. code-block:: c#
    :linenos:

    [Serializable]
    public class CreateSubEstimatesFromProjectDisciplinesDto
    {
        public Guid JobTypeId { get; set; }
        public IEnumerable<CreateSubEstimatesFromProjectDisciplinesDepartmentDto> Departments { get; set; }
    }

    [Serializable]
    public class CreateSubEstimatesFromProjectDisciplinesDepartmentDto
    {
        public Guid Id { get; set; }
    }

    if (!(Document is IEstimateObject estimate) || estimate.ProjectObject == null)
        return ActionResult.Success();
    var templates = await Host.GetTemplatesAsync(0, 100, "CreateSubEstimatesFromProjectDisciplines", null, estimate.JobTypeObject.Id.ToString(), null);
    if (estimate.ProjectObject == null)
        return ActionResult.Success();
    if (templates.Count() == 0)
    {
        var departments = await Host.GetDepartmentsAsync("", null, null, estimate.ProjectObject.Id);
        foreach (var department in departments)
        {
            var jobType = department.JobTypesList.FirstOrDefault(jt => jt.Active);
            if (jobType == null) continue;
            var newEstimate = Host.CreateEstimate();
            newEstimate.ContractObject = estimate.ContractObject;
            newEstimate.ProjectObject = estimate.ProjectObject;
            newEstimate.CompanyObject = department.CompanyObject;
            newEstimate.DivisionObject = department.DivisionObject;
            newEstimate.DepartmentObject = department;
            newEstimate.JobTypeObject = jobType;
            newEstimate.ClientObject = estimate.ClientObject;
            newEstimate.CommercialPaymentConditionObject = estimate.CommercialPaymentConditionObject;
            newEstimate.BrandObject = estimate.BrandObject;
            newEstimate.ProductObject = estimate.ProductObject;
            newEstimate.CurrencyObject = estimate.CurrencyObject;
            newEstimate.Exchange = estimate.CurrencyObject?.Sell ?? 1;
            newEstimate.EstimateTypeId = estimate.EstimateTypeId;
            newEstimate.ParentEstimateObject = estimate;
            newEstimate.IgnoreChanges = false;
            newEstimate.Name = estimate.Name + " - " + department.Name;
            newEstimate.DocumentTypeObject = estimate.DocumentTypeObject;
        }
    }
    else
    {
        var template = templates.First();
        var details = Host.DeserializeObject<CreateSubEstimatesFromProjectDisciplinesDto>(template.Details.ToString());
        if (details == null) return ActionResult.Success();
        var projectDepartments = await Host.GetDepartmentsAsync("", null, null, estimate.ProjectObject.Id);
        var detailsDepartmentsIds = new HashSet<Guid>(details.Departments.Select(d => d.Id));
        foreach (var detailDepartment in projectDepartments.Where(d => detailsDepartmentsIds.Contains(d.Id)))
        {
            var jobType = await Host.GetJobTypeByIdAsync(details.JobTypeId);
            var department = await Host.GetDepartmentByIdAsync(detailDepartment.Id);
            if (department == null || jobType == null) continue;
            var newEstimate = Host.CreateEstimate();
            newEstimate.ContractObject = estimate.ContractObject;
            newEstimate.ProjectObject = estimate.ProjectObject;
            newEstimate.CompanyObject = department.CompanyObject;
            newEstimate.DivisionObject = department.DivisionObject;
            newEstimate.DepartmentObject = department;
            newEstimate.JobTypeObject = jobType;
            newEstimate.ClientObject = estimate.ClientObject;
            newEstimate.CommercialPaymentConditionObject = estimate.CommercialPaymentConditionObject;
            newEstimate.BrandObject = estimate.BrandObject;
            newEstimate.ProductObject = estimate.ProductObject;
            newEstimate.CurrencyObject = estimate.CurrencyObject;
            newEstimate.Exchange = estimate.CurrencyObject?.Sell ?? 1;
            newEstimate.EstimateTypeId = estimate.EstimateTypeId;
            newEstimate.ParentEstimateObject = estimate;
            newEstimate.IgnoreChanges = false;
            newEstimate.Name = estimate.Name + " - " + department.Name;
            newEstimate.DocumentTypeObject = estimate.DocumentTypeObject;
        }
    }
    return ActionResult.Success();


**Template**

| This action requires a Job Type template, with a structure similar to the one below.
| Each object contains the JobTypeId along with a list of the Departments, each with the Id. This way, only the added Departments will generate an Estimate.

.. code-block:: json
    :linenos:

    {
        "name": "CreateSubEstimatesFromProjectDisciplines Example Template",
        "type": "CreateSubEstimatesFromProjectDisciplines",
        "documentTypeName": null,
        "documentId": "b21572ab-e2a9-4789-8ec1-31f1e4377e88",
        "editorWorkspaceId": null,
        "editorWorkspaceName": null,
        "category": "",
        "layout": "",
        "description": "JobType",
        "details": {
            "JobTypeId": "b21572ab-e2a9-4789-8ec1-31f1e4377e88",
            "Departments": 
            [
                {
                    "Id": "7D7C827F-511B-44D4-BDDC-9948B05C636E"
                },
                {
                    "Id": "E6E2B7F5-5D59-4682-935F-69D2F96620AC"
                }
            ]
        }
    }