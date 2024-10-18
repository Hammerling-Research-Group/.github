# Standards for Collaborative Computing & Development
### Hammerling Research Group, Colorado School of Mines

## Contents
- [Introductory Remarks & Mission](#introductory-remarks--mission)
- [Philosophy Guiding Code Development](#philosophy-guiding-code-development)
- [Collaborating on Code for Shared Research Goals](#collaborating-on-code-for-shared-research-goals)
- [Practical Guidelines for Collaborative Development](#practical-guidelines-for-collaborative-development)
  - [GitHub Workflow](#github-workflow)
    - [Central Organization Structure](#central-organization-structure)
    - [Branching Strategy](#branching-strategy)
    - [Pull Requests (PRs)](#pull-requests-prs)
    - [Direct Commits](#direct-commits)
  - [Code Quality and Linting](#code-quality-and-linting)
    - [Code Standards](#code-standards)
    - [Testing](#testing)
    - [Automated Linting and Continuous Integration (CI)](#automated-linting-and-continuous-integration-ci)
    - [Human Peer Review](#human-peer-review)
  - [Versioning and Documentation](#versioning-and-documentation)
    - [Version Control](#version-control)
    - [Documentation Standards](#documentation-standards)
  - [Flexibility and Adaptability in Development](#flexibility-and-adaptability-in-development)
    - [Allowing Exploration](#allowing-exploration)
    - [Experimental Branches in Production Repos](#experimental-branches-in-production-repos)
- [Best Practices for Distributed Work](#best-practices-for-distributed-work)
  - [Regular Check-ins](#regular-check-ins)
  - [Documentation for Remote Onboarding](#documentation-for-remote-onboarding)
  - [Encouraging Contributions](#encouraging-contributions)

## Introductory Remarks & Mission
 
This document sets out the standards for what it means to 1) be a team member in the *Hammerling Research Group*, and 2) develop and collaborate with and through research code at a minimum. Everything we do re: computing, research code and development flows from this guiding mission:

> *In the Hammerling Research Group, we strive to develop flexible, reproducible, and scalable code to support the academic goals of the group. Our computing and development context involves distributed members and teams working asynchronously, contributing to a central GitHub organization.* 

The goal of the standards outlined in this document is meant to guide team members on the *minimum* set of best practices and expectations for collaborating effectively while ensuring code quality and fostering a culture of open, shared research computing.

## Philosophy Guiding Code Development

In the Hammerling Research Group (hereafter, *HRG*), we appreciate that everyone has a unique approach to working and developing code. While we respect and encourage these differences to keep creativity and productivity thriving, any and all code or work involving any project in HRG must adhere to our unified philosophy to keep us all moving as a unit toward our mission. That is, our code should be:

  - *Reproducible*: Each research output must be accompanied by code that others can use to generate the *same* results.

  - *Collaborative*: Codebases should be open for contributions and improvements. Everyone's work benefits from the expertise of others.

  - *Scalable & Flexible*: Code should be designed to easily accommodate changes and additions without requiring major rework, whether for academic extensions or real-world applications.

  - *Version Controlled*: Code should be well-documented and versioned in such a way that others can follow the evolution of the project and contribute responsibly.

## Collaborating on Code for Shared Research Goals

Research computing is inherently a collaborative effort, though it can often drift into isolated, myopic processes. To guard against the threat of isolation, and instead foster strong community in and among all HRG members, our individual and collective efforts should support the following principles:

  - *Respectful Peer Review*: Every major contribution is reviewed by at least one other *human* team member to ensure accuracy, clarity, and adherence to standards. This not only complements automated checks, tests, and CI more broadly, but it also creates opportunities for learning and catching issues early, as well as creating a sense of community in our work.
  
  - *Shared Codebase Ownership*: Related to the previous principle, even though specific projects or pieces of code might be developed by individual researchers, the responsibility for the code rests with the team. Everyone is encouraged to contribute ideas, fixes, and improvements. The simplest way to implement this principle is to "watch" every repo/project, and contribute when able.
  
  - *Open Communication*: In line with open *development*, open *communication* fosters wider and stronger community among team members. To this end, use issues, discussions, and other communication tools like Slack to share updates, ideas, or blockers in development to keep everyone aligned on project progress.
  
## Practical Guidelines for Collaborative Development

### GitHub Workflow

In this section, we address key concepts aimed at understanding the structure and basics of how we develop on GitHub. 

#### Central Organization Structure

We will have two complementary spaces for code and development within our central organization: 

  - *Project-Specific Repos*: Dedicated repositories (aka "repos") will serve as the *production*/stable versions of code for a given project (e.g., `dlq`). These should contain the most up-to-date, tested, and reproducible versions of the models and code.
  
  - *Personal Repos/Workspaces*: In parallel, each team member may choose to develop and maintain a personal repo within the organization to develop features, experiment, or test new ideas. These are meant to be personal staging areas.

#### Branching Strategy

The HRG leverages development branches to make contributions or changes to production code, to ensure nothing breaks in the stable version while working on and integrating new features to codebases.

  - *Feature Branches*: All code changes should start on a feature branch. Team members create branches for each new feature, bug fix, or experiment (`feature/experiment_x`, `bugfix/issue_y`). This allows for parallel development without impacting the production code.

  - *Main/Production Branch*: The main branch in each project repo is reserved for stable, tested, and reviewed code. Only code that has passed quality checks *and* human code review, should be merged here.

**Note:** See the quick start guide, *Getting Started with Branching*, for branch-based development details and best practices. 

#### Pull Requests (PRs)

When a feature or fix is ready to merge, members should submit a pull request (PR) from the feature branch to the production repository’s main branch.

Each PR must pass all automatic tests before merging (which are triggered when the PR is opened), and also should be reviewed by at least one other team member.

Importantly, in each PR, member's should include a clear summary of what was changed and any other relevant notes in the `comments` field of the PR.

**Note:** See the quick start guide, *Getting Started with Pull Requests*, for pull requests details and best practices. 

#### Direct Commits

**_Direct commits to the main branch are discouraged_** and will likely be sent back to the member for routing through the proper channels. That is, all changes should go through the branching and PR process to ensure peer review and maintain the integrity of the production code.

### Code Quality and Linting

In this section, we address key concepts aimed at ensuring code is of sufficient quality to merge to the main/production branch. 

#### Code Standards

Consistency makes the code easier to read, understand, and maintain.

Follow a standardized style guide. At present this inlcudes the following conventions at a minimum:

  - Functions, repos and other object names should be in lower case, e.g., `dlq`. Names that must be joined, should be joined by `_`, e.g., `puff_model`.

  - Use meaningful variable names and clear, concise comments to explain complex logic. 

  - Avoid commenting directly in the code. Complementary documentation (discussed more below) should provide all needed context for successfully running and contributing to codebases. 

#### Testing

All major changes or features should include corresponding tests. Unit testing helps ensure the robustness of the code and reduces the likelihood of bugs in production. 

While our automated checks for code coverage will encourage wide coverage (e.g., >= 70%), we ultimately want *meaningful* unit tests, even at the cost of slightly lower coverage. 

#### Automated Linting and Continuous Integration (CI)

All code should pass a linter *before* submission. Automating CI of this sort via GitHub actions, linting workflows will use tools such as `lintr` (for R) or `pylint` (for Python) to enforce code style and highlight potential issues.

#### Human Peer Review

Once cleared the automated checks and tests successfully to root out and address technical issues, all code submissions will be assigned a human peer reviewer. 

The goal is to complement the automated checking to ensure that, at an intuitive and practical level, the code comports with the goals and mission of HRG and is doing what it is purported to be doing. These types of "gut checks" are often overlooked in purely automated checking processes. 

**Note:** See the quick start guide, *Getting Started with Code Review*, for best practices relating to conducting rigorous, open code review. 

### Versioning and Documentation

#### Version Control

If you're maintaining a production repo, use semantic versioning (e.g., `v0.1.0`) for releases of major models or codebases.

At a minimum, noting the change in the PR documentation is expected. Ideally, and especially for major revisions or changes in logic, bump the version appropriately and document the changes in a `CHANGELOG.md` or `NEWS.md` file. 

#### Documentation Standards

All functions, models, and scripts should be documented using `Roxygen` (for R) or `Sphinx` (for Python). This ensures that others can easily understand the code without needing to dive into its implementation. It also ensures consistency in documentation.

Keep an up-to-date `README` in each repo, outlining the project, dependencies, and how to use/run the code locally. 

Include a minimal working example that shows how to use the code and what should be expected as output. Ideally this is in a separate subdirectory within the repo (e.g., `repo_name/vignettes/ex.R`), though in simpler cases, including this in the `README` would work too.

### Flexibility and Adaptability in Development

#### Allowing Exploration

Individual workspaces (personal repos) are spaces for team members to explore ideas, develop new features, and experiment with different methods or models. However, code should only be integrated into the production repos *after* peer review and successful testing via branching as previously noted.

#### Experimental Branches in Production Repos

Experimental branches can be created in the production repos to serve as temporary workspaces for collective experimentation on specific ideas. These branches should be clearly labeled as experimental and *not* considered stable. Once stable, members should follow standard branching, PR, and checking processes previously addressed. Again, see the *Getting Started with Branching* and *Getting Started with Pull Requests* quick start guides for more on the full contribution process.

## Best Practices for Distributed Work

Importantly, HRG work is done in a distributed setting. That means, members may work from home, on campus, or a blend of these. This section, then, includes some best practices to ensure our community of development remains strong, and also that our work is being done and integrated into the broader HRG as intended.   

### Regular Check-ins

It is strongly encouraged to schedule regular check-ins with appropriate team members based on a given project and/or active development of some set of code. These are useful for discussing progress, blockers, and code reviews in person (especially when disagreement occurs). 

On GitHub explicitly, HRG uses *GitHub Projects* to track code and development progress, assign issues, and manage deadlines.

### Documentation for Remote Onboarding

New team members will have access to clear documentation on how to set up their local environments, contribute from workspaces to production code bases, and follow the contribution standards set out in this document. The primary documents will include: 

  - *Standards for Collaborative Computing & Development* (this document)
  - *Contributor Code of Conduct*
  - All *Quick Start* guides developed by and for the HRG

### Encouraging Contributions

As noted throughout, research computing of the sort that we do in HRG is collaborative and communal. As such, *everyone* on the team is encouraged to contribute ideas, suggest improvements, or identify potential areas of optimization. The simplest way to engage in development is via repo-specific issues. Slack should be used for more informal ideation that may or may not be directly related to code and development. 
