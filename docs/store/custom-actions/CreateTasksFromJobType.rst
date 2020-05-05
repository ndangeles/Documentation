CreateTasksFromJobType
======================

**When to use**

There was a need to create tasks directly from Job Type.
Add this action to a the workflow transition to create automatically tasks.

**Syntax**

The following is the C# statement.

.. code-block:: c#
    :linenos:

    [Serializable]
    public class CreateTasksFromJobTypeDto
    {
        public IEnumerable<CreateTasksFromJobTypeTaskDto> Tasks { get; set; }
    }

    [Serializable]
    public class CreateTasksFromJobTypeTaskDto
    {
        public int DurationMinutes { get; set; }
        public string Subject { get; set; }
        public string DepartmentName { get; set; }
        public string JobTypeName { get; set; }
        public bool IsDeliverable { get; set; }
    }

    if (!(Document is IJobObject job))
        return ActionResult.Success();
    var templates = await Host.GetTemplatesAsync(0, 100, "CreateTasksFromJobType", null, job.JobTypeObject.Id.ToString(), null);
    if (templates.Count() == 0)
    {
        return ActionResult.Success();
    }
    else
    {
        var template = templates.First();
        var detail = Host.DeserializeObject<CreateTasksFromJobTypeDto>(template.Details.ToString());
        foreach (var task in detail.Tasks)
        {
            var jobType = (await Host.GetJobTypesAsync("", task.JobTypeName)).FirstOrDefault();
            var department = (await Host.GetDepartmentsAsync(task.DepartmentName)).FirstOrDefault();
            if (department == null || jobType == null) continue;
            var newJob = Host.CreateJob();
            newJob.ParentJobObject = job;
            newJob.Subject = task.Subject;
            newJob.DepartmentObject = department;
            newJob.JobTypeObject = jobType;
            newJob.IsDeliverable = task.IsDeliverable;
        }
    }
    return ActionResult.Success();
