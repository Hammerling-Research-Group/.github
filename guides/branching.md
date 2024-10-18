---
title: "Getting Started with Branching"
subtitle: "Hammerling Research Group (HRG) // Quick Start Guide"
format: pdf
toc: false
---

## Introductory Remarks

This quick start guide is intended to get unfamiliar team members up to speed on the basics of working with branches to support the work of HRG. 

Instead of forking the production repository as some may be familiar with, team members can instead clone repositories and set up feature branches within the same central repository, each of which is aimed at addressing a specific feature or fix to the production code. 

*The bottom line:*

  - *No forking required*: All development happens on branches created within the "production" repo.

  - *Branch for each change/feature*: Each new feature or change is developed on a separate branch (e.g., `feature/method_x`). This keeps the main branch stable.

  - *PR review process*: PRs ensure that every contribution is human-reviewed, passes tests, and meets coding standards before being integrated into the production code.

Ultimately, we've adopted this workflow in HRG to ensure the production code stays stable, while allowing individual team members to work freely in parallel on their contributions, test thoroughly, and integrate changes in a controlled and reproducible manner, in line with open development best practices.

Let's unpack this with an example. 

## The Setup

Suppose we are working in the HRG organization. In this organization is a repo called `model_1`, which contains the production version of the code to implement `model_1`

Philip, a member of HRG, wants to contribute a new feature to `model_1` from his personal workspace (a repo called `workspace_philip`), which is also within the HRG organization.

## The Steps

  1. Philip will clone the production repo to his local machine so he can work with the most up-to-date code. Using the command line, this might look something like: 

```{bash}
git clone https://github.com/HRG/model_1.git
cd model_1
```

Or, via <https://github.com/>: Click the `Code` button, choose `HTTPS`, and copy the URL. Then clone it using the command above, or by pasting in a new RStudio project. 


  2. Next, Philip creates a new branch specifically for the feature he is working on. For example, he's adding a new method called `method_x`.

```{bash}
git checkout -b feature/method_x
```

Or, via <https://github.com/>: Go to <https://github.com/team-org/model_1/branches>. Click "New branch" or click on the existing branch dropdown, and type `feature/method_x`. Create the branch and switch to it locally with the above command or within RStudio. 


  3. Now Philip can make his changes locally. He adds the new method and tests it thoroughly in his local environment, via RStudio (or some other IDE). After testing, he stages and commits the changes:

```{bash}
git add .
git commit -m "Added method_x for better analysis of y"
```

Alternatively, Philip could stage and commit directly via RStudio (or GitHub Desktop, etc.) if preferred.

\newpage 

  4. Philip then pushes the `feature/method_x` branch to his personal workspace repo within the HRG organization:

```{bash}
git push origin feature/method_x
```

Or, via <https://github.com/>: Philip navigates to his personal workspace repo (e.g., <https://github.com/team-org/philip_model_1>), and pushes from there.


  5. After pushing his branch, Philip goes to GitHub, navigates to the `model_1` repo, and creates a pull request. The pull request compares his `feature/method_x` branch with the main branch of the production repository (`model_1`). Via the website approach, go to <https://github.com/team-org/model_1/compare>. Then, Philip selects the feature branch `feature/method_x` and chooses the production repo's main branch for comparison. He can fill in the PR description and provide a summary of changes before submitting the PR, e.g.:

> *Added method_x for analyzing y in more detail. Implemented using [algorithm_x]. Tests included for checking edge cases.*


  6. Opening the PR will automatically start the linting workflow via GH Actions. GH Actions runs the automated tests and linting rules setup by HRG on the PR to ensure Philip's code doesn't break anything or introduce stylistic errors. These tests must pass before progressing to the next step.


  7. Once passed linting and automated checks, a team member is assigned to review Philip’s PR. The member reviews the changes in the code, ensures it follows best practices, and checks that it passes all linting and automated tests. If there are suggestions or fixes needed, the team member leaves comments on the PR, and Philip can then address them by making changes locally, committing, and pushing updates to the same `feature/method_x` branch. The PR is automatically updated, and the linting starts again. 


  8. Once the full set of checks and review are complete and tests pass, the member who reviewed the code (or some other authorized team member) approves and merges the pull request into the main branch of the production repo. The new feature (`method_x`) is now part of the production codebase, and is considered *stable*.


  9. It is often a good idea, though not required, to clean up a bit after the PR is merged. For example, Philip may delete the `feature/method_x` branch both locally and from his org workspace repo to keep things tidy. For example:

```{bash}
git branch -d feature/method_x
git push origin --delete feature/method_x
```

