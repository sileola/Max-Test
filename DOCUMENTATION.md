
___
## TASK: TO SET UP A CI PIPELINE ON A TODO APP USING GITHUB ACTIONS
___

Overview: This task is aimed a configuring a GitHub Actions workflow that can build and test  a ToDo application written with Nodejs. The workflow will also test for the integrity of the application. 

The entire workflow is shown in the image below:

![CI WORKFLOW IMAGE](./images/workflow.PNG 'Entire CI Workflow')
The following sections explain, in further details, the salient points of the workflow shown above.


*  **name: CI PIPELINE FOR A TODO APP**

    This input to this syntax is optional however, it is a good practice to give a concise but descriptive overview of what the entire workflow intends to achieve.

*       on:
            push:

                branches: [ "main" ]

            pull_request:

                branches: [ "main" ]

    The section above decribes the event that should trigger the workflow. In this case, the workflow is triggered anything someone pushes to the "main" branch or everytime a pull request is created with 'main' branch as a target.


