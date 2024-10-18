# Getting Started with Pull Requests
### Hammerling Research Group, Colorado School of Mines

## Introductory Remarks

This quick start guide is intended to get team members up to speed on the process of creating and managing pull requests (PRs) for HRG's code development workflow. Pull requests are the primary means by which code is contributed to the HRG production code. As such, they ensure that every contribution to the production code is reviewed, tested, and meets coding standards. Much of this is covered in the *Getting Started with Branching* guide. 

Each team member works on a feature or development branch, *not* the `main` branch to avoid braking the production code, before contributing to the production repo (e.g., `model_1`) through a PR.

Of note, if not already done, each team member should first review the HRG Standards of Development doc for justification and motivation behind a lot of the content in ths quick start guide. 

*The bottom line:*

  - *PRs are required*: Every code contribution to a production repo happens through a PR. *No direct commits* to production code are allowed, in line with HRG standards.
  
  - *Human review is key*: A PR must be reviewed by at least one other team member before it can be merged. This ensures code quality and stability, as well as intuitive human-readable design and structure.
  
  - *Automated checks*: PRs trigger automated linting (testing workflows) to ensure code correctness and consistency with HRG's standards.

Let's walk through an example of creating a pull request.

## The Setup

Imagine that team member Philip is working on adding a new feature to the production repository `model_1`. The steps below describe how he will prepare and submit a pull request, which is instructive because it captures the vast majority of pull request use cases in an organizational and collaborative development setting like HRG. 

## The Steps

  1. Philip begins by working on his feature branch. Once he's ready to contribute this work to the production repository (`model_1`), which we can call `method_x` as a new feature of the model, he first makes sure that his branch is up-to-date with the latest version of `model_1`:

```{bash}
git fetch origin
git rebase origin/main
```

This process, called `pulling`, *guarantees* that his changes will integrate smoothly with any updates made to the production repo while he's been working. Its good practice to *always pull before pushing*. Even pull multiple times during active development. 


  2. Next, Philip pushes his feature branch:

```{bash}
git push origin feature/method_x
```

Or, as with most actions, he can do this via GitHub Desktop, RStudio, or the GitHub website directly via point-and-click.


  3. Now, he's ready to create a pull request to suggest that his changes on his branch be merged to the `main` production branch. For example, on <https://github.com/>, Philip navigates to the HRG production repo `model_1` and clicks on "Compare & pull request." GitHub will automatically compare his branch (`feature/method_x`) to the `main` branch of `model_1`. In practical terms, the maintainer of the production version of `model_1` is comparing changes to the `main` branch, and then decides whether to grant the request to *pull* in changes from the dev branch and merge those changes to the production version, or not. This decision takes shape through a code review. See the *Getting Started with Code Reviews* guide for more. 

  
 
  4. Philip writes a detailed description of the changes in the pull request comments box. This should include, at a minimum:
  
      - The purpose of the feature/fix (e.g., *Implemented `method_x` to improve performance on `y`*)
      
      - Any tests that were performed and their results
      
      - Links to any relevant issues or discussions (via `#`)
  
  
  5. After opening the PR, GitHub Actions (GH Actions) will automatically trigger the configured testing workflow (i.e., CI or linting). These tests will vary by repo and include any combination of: unit tests, integration tests, and basic linting checks. Either way, the automated checks will be focused on ensuring the new code complies with HRG's standards and won't break existing functionality.
  
  
  6. Once the automated checks pass, the PR is ready for human review, which is discussed at length in the *Getting Started with Code Review* guide.

  
  7. The reviewer may leave comments or request changes. If so, Philip needs to first address these comments by making the necessary changes locally, committing them, and pushing to the same `feature/method_x` branch, which in effect is a redo of steps 1-5. Recall, when any PR is created, it triggers the automated checks. So, even though it may have just recently occurred, GH Actions will again automatically update the PR and rerun the tests.
  
  
  8. Once the reviewer is satisfied and the tests pass, they approve the pull request and then merge the changes on the dev branch into the `main` branch of `model_1`.
  
  
  9. After the PR is merged, Philip may (probably should) clean up by deleting the feature branch both locally *and* remotely. This might look as simple as: 

```{bash}
git branch -d feature/method_x
git push origin --delete feature/method_x
```

This helps keep the repo tidy and prevents clutter from unnecessary branches. This step is not required per HRG standards, but its a generally good habit to form in these types of collaborative, active development settings. 

## Best Practices for Pull Requests

We will wrap up with a few thoughts on some best practices to keep in mind, some of which were mentioned in the steps above:

  - Keep PRs small and focused. A pull request should ideally introduce a single change or feature, making it easier to review and test.
  
  - Write clear PR descriptions. This helps reviewers (*and future you*) understand the purpose and scope of your changes.
  
  - Use meaningful commit messages. Make sure each commit explains what was changed and why, though the length of these are capped by GitHub with the goal of forcing brevity.
  
  - Keep your branch up-to-date. Regularly sync your feature branch with the main branch to minimize merge conflicts. This has the added benefit of potentially prompting new contribution ideas if you detect something that may require a bit more attention. 
