
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

*       jobs:
            build:

    This is the part that gets executed when the workflow is triggered. A workflow run is made up of one or more jobs that can run sequentially or in parallel. This workflow contains a single job and the job is called 'build'


* **runs-on: ubuntu-latest**

    This syntax describes type of runner(or Operating System) that the job will run on. This job will run on Linux. You can change the runs-on key to run your jobs on a different operating system. For Windows and MacOS, the syntax is `runs-on: windows-latest` and `runs-on: macos-latest` respecetively.


*       strategy:
            matrix:
             node-version: [14.x, 16.x, 18.x]
    This syntax is used to specify the Nide.js version using a matrix strategy (Node.js version can also be specified using the `setup-node` action).
    
    This workflow includes a matrix strategy that builds and tests the code with three Node.js versions: 14.x, 16.x and 18.x. The 'x' is a wildcard character that matches the latest minor and patch release available for a version. Each version of Node.js specified in the node-version array creates a job that runs the same steps.


* **Steps:**

    Steps represent a sequence of tasks that will be executed as part of the job.
      
        steps:
          - uses: actions/checkout@v3
          - name: Use Node.js ${{ matrix.node-version }}
            uses: actions/setup-node@v3
            with:
                node-version: ${{ matrix.node-version }}
                cache: 'npm'
          - run: npm ci
          - run: npm run build --if-present
          - run: npm test
    1. The `actions/checkout@v3` syntax checks-out the repository under $GITHUB_WORKSPACE, so the job can access it
    
    2. The `actions/setup-node@v3`helps to optionally download and cache the distribution of the requested Node.js version; helps to optionally cache npm dependencies and helps to register problem matchers for error output

    3. Installing dependencies: NPM – or "Node Package Manager" – is the default package manager for JavaScript's runtime Node.js. The `npm` was used to install dependencies in the workflow before building and testing the code.
    4. The `npm ci` is used for clean install. This command is similar to `npm install`, except it is meant to be used in automated environments such as test platforms, continuous integration, and deployment -- or any situation where you want to make sure you're doing a clean install of your dependencies.
    5. Buidling the code:

         `npm run build --if-present`

        The command above is used to run/build the TODO app.

    6. Testing the code:
       
         `run: npm test`

    The command above is used to run test.

The CI pipeline was successful and the repo link is provided below:

    [CI Repo link](https://github.com/sileola/Max-Test.git)