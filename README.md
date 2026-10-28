Experiment: CI Pipeline Using GitHub Actions
1. Aim

To implement a Continuous Integration (CI) pipeline using GitHub Actions that automatically checks Python code whenever changes are pushed to GitHub.

2. Objectives
Understand Continuous Integration (CI).
Create and upload a project to GitHub using Git.
Configure a CI workflow using a YAML file.
Automatically check Python syntax when code is pushed.
Observe the pipeline execution results in GitHub Actions.
3. Software Requirements
Git
GitHub account
Python 3
Web browser
Text editor or VS Code
4. Theory

Continuous Integration (CI) is a DevOps practice in which code changes are automatically checked whenever developers push code or open pull requests.

Git is used for version control, GitHub stores the project repository, and GitHub Actions executes automated workflows.

A workflow is configured using a YAML file stored at:

.github/workflows/ci.yml

The workflow specifies when the pipeline runs and which commands it executes.

5. Procedure
Step 1: Create a project

Create a folder named ci-practical and open a terminal inside it.

bash
mkdir ci-practical
cd ci-practical
git init

Step 2: Create a Python file

Create a file named hello.py and add the following code:

python
a = 10
b = 10

if a == b:
    print("Values are equal")

Step 3: Upload the project to GitHub

Configure Git if you have not already done so:

bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"


Stage and commit the file:

bash
git add .
git commit -m "Initial commit"


Create an empty repository named ci-practical on GitHub.

Connect the local repository to GitHub and push the code. Replace the URL with your actual repository URL.

bash
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/ci-practical.git
git push -u origin main

Step 4: Create the CI workflow file

Inside the project, create the following directory structure:

text
ci-practical/
├── hello.py
└── .github/
    └── workflows/
        └── ci.yml


The file can be created locally using VS Code or directly through the GitHub website by selecting Add file → Create new file.

Enter this path as the filename:

.github/workflows/ci.yml

Step 5: Configure the CI pipeline

Add the following code to ci.yml:

yaml
name: Python CI Pipeline

on:
  push:
  pull_request:

jobs:
  build-and-check:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Check Python syntax
        run: python -m compileall -q .


Explanation of the workflow:

name: Specifies the workflow name.
on: Defines the events that trigger the workflow.
push: Runs the workflow when code is pushed.
pull_request: Runs the workflow for pull request events.
jobs: Defines the tasks to execute.
runs-on: Selects the Ubuntu runner.
steps: Lists the actions and commands to execute.
actions/checkout: Retrieves the repository code.
actions/setup-python: Sets up Python.
compileall: Checks the syntax of Python files.
Step 6: Commit and push the workflow

If you created the file locally, run:

bash
git add .
git commit -m "Add CI workflow"
git push


If you created the file directly on GitHub, commit the new file through the GitHub interface.

Step 7: Verify the pipeline
Open the GitHub repository.
Click the Actions tab.
Select the Python CI Pipeline workflow.
Open the latest workflow run.
Check whether the workflow completed successfully.

A green check mark indicates that the configured steps passed. A red cross indicates that a step failed.

Step 8: Test the pipeline with another change

Modify hello.py and add:

python
print("CI pipeline demonstration")


Commit and push the change:

bash
git add hello.py
git commit -m "Update Python program"
git push


Open the Actions tab again and verify that a new workflow run starts.

Step 9: Demonstrate error detection

Temporarily introduce a syntax error in hello.py:

python
if a == b
    print(a)


Commit and push the incorrect code. The syntax-check step should fail.

Correct the code by adding the missing colon:

python
if a == b:
    print(a)


Commit and push the correction. The workflow should run again and pass.

Note: The syntax-check command detects syntax errors, but it does not execute the program or verify its logical correctness.

6. Result

A CI pipeline was configured using GitHub Actions. The workflow automatically ran on push and pull request events, checked Python syntax, and displayed the execution status in the GitHub Actions interface.

7. Advantages
Automates code checking.
Detects syntax errors early.
Reduces repetitive manual checks.
Provides consistent feedback after code changes.
Supports collaborative software development.
8. Conclusion

The Continuous Integration pipeline was successfully demonstrated using GitHub Actions and a YAML configuration file. Code changes pushed to GitHub triggered the workflow, which checked Python syntax and reported whether the configured checks passed or failed.

9. Viva Questions

Q1. What is CI?

Continuous Integration is the practice of automatically building and checking code changes.

Q2. What is Git?

Git is a distributed version control system used to track changes in files.

Q3. What is GitHub?

GitHub is an online platform for hosting Git repositories and collaborating on code.

Q4. What is GitHub Actions?

GitHub Actions is a platform for automating workflows, including CI and CD.

Q5. What is a YAML file?

YAML is a human-readable data serialization format used to configure workflows and other applications.

Q6. What is the purpose of ci.yml?

It defines the workflow triggers, jobs, and steps that GitHub Actions executes.

Q7. What happens when code is pushed to GitHub?

If the push matches the workflow triggers, GitHub Actions starts the configured workflow.

Q8. What does a green check mark mean?

It means the workflow completed successfully and its required steps passed.

Q9. Does the syntax check execute the Python program?

No. The compileall command checks syntax; it does not run the program's normal logic.

Q10. What is the difference between CI and CD?

CI focuses on integrating and checking code changes. CD extends automation toward delivering or deploying software.
