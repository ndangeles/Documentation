CreateSubEstimatesFromProjectDisciplines
========================================


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
    var templates = await Host.GetTemplatesAsync(0, 100, ""CreateSubEstimatesFromProjectDisciplines"", null, estimate.JobTypeObject.Id.ToString(), null);
    if (estimate.ProjectObject == null)
        return ActionResult.Success();
    if (templates.Count() == 0)
    {
        var departments = await Host.GetDepartmentsAsync("""", null, null, estimate.ProjectObject.Id);
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
            newEstimate.Name = estimate.Name + "" - "" + department.Name;
            newEstimate.DocumentTypeObject = estimate.DocumentTypeObject;
        }
    }
    else
    {
        var template = templates.First();
        var details = Host.DeserializeObject<CreateSubEstimatesFromProjectDisciplinesDto>(template.Details.ToString());
        if (details == null) return ActionResult.Success();
        var projectDepartments = await Host.GetDepartmentsAsync("""", null, null, estimate.ProjectObject.Id);
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
            newEstimate.Name = estimate.Name + "" - "" + department.Name;
            newEstimate.DocumentTypeObject = estimate.DocumentTypeObject;
        }
    }
    return ActionResult.Success();