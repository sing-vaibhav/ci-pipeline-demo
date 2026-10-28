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
`
