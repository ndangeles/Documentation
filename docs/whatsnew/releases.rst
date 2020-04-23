Releases
========

20.6
----

The dataGrid was not working properly
+++++++++++++++++++++++++++++++++++++

    **Cause**

    It was found an issue on the dataGrid where loading data.

    **Prevent Future Issues**

    Not applied.

    **Configurations**

    In back-office, the administrator under Maintenance/Document Member 
    should add field “Company” to each document type (i.e. Job and Estimate) 
    to the Role (Requester Profile) assigned to Users who create Jobs and Estimates.

    **Proposed Tests**

        1. In back-office, administrator adds “Company” as Document Member for document types Deliverable and Estimate for Role (e.g. Estimavesave) assigned to users who create Jobs and Estimates.

        2. User creates Job and Estimate

        3. Check if Company and Department are shown as separate dropdown fields in Job and Estimate creation popup windows

        4. Check if default value for Company is the home company of the user

        5. Check that dropdown selections for Company are the companies the user has access to

        6. Check that dropdown selections for Department are the plannable departments under the Company previously selected

        7. Verify if “Company” is included in the Column Chooser for the Job and Estimate List page

    **Historical data**

    Not applied.

20.5
----