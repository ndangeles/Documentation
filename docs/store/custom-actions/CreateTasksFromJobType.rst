CreateTasksFromJobType
======================

**Compatible documents**
Job

**When to use**

There was a need to create tasks (Jobs) directly from the Job Type.
Add this action to a the workflow transition to create automatically tasks.
(Remember: This code is the default implementation which can be modified anytime in the system)

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


**Template**

| This action requires a Job Type template, with a structure similar to the one below.
| Each object inside the Tasks list contains the Subject, DepartmentName, JobTypeName and IsDeliverable properties. For each of these objects, a Job will be created with the defined properties.

.. code-block:: json
    :linenos:

    {
        "name": "CreateTasksFromJobType Example Template",
        "type": "CreateTasksFromJobType",
        "documentTypeName": null,
        "documentId": "b21572ab-e2a9-4789-8ec1-31f1e4377e88",
        "editorWorkspaceId": null,
        "editorWorkspaceName": null,
        "category": "",
        "layout": "",
        "description": "JobType",
        "details": {
            "Tasks": [
                {
                    "Subject": "Concert Hall",
                    "DepartmentName": "Account Management",
                    "JobTypeName": "Radio",
                    "IsDeliverable": false
                },
            {
                    "Subject": "Concert Hall 2",
                    "DepartmentName": "Interactive Production",
                    "JobTypeName": "Other",
                    "IsDeliverable": false
                }
            ]
        }
    }