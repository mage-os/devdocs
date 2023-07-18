# Contributor & Reviewer Guide
Mage-OS guidelines for code contributors and reviewers.

## Code contributions
Mage-OS operates an open contributor model: anyone is welcome and needed to contribute to development, review, and testing. 

Though, some hierarchy is needed to guarantee that the process runs smoothly. Thus, there are some people with higher privileges for merging pull requests. We call them Mage-OS maintainers. 

Everyone can become a Mage-OS maintainer based on the trust earned from the community over time.

### Contribute to Mage-OS source code
We adopt a [fork and pull model](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/about-collaborative-development-models#fork-and-pull-model) to contribute to the Mage-OS codebase. This method allows a contributor to maintain a copy of the forked codebase and quickly sync it with the base copy. 

To merge a set of changes from the fork into the main repository, the contributor submits a pull request from the owned fork to the base repository.

The kind of expected contributions:
new features in the form of new extensions, hereinafter Mage-OS features
changes to fix and improve Mage-OS features
changes to fix and improve tests
new tooling
changes to fix and improve existing tooling
documentation

Reviewers will review the submitted pull requests by interacting with contributors through the GitHub platform. In case the contributor is not able to provide needed feedback, the reviewers are free to decide whether to close the pull request or ask other contributors to carry it out.

We recommend new contributors familiarize themselves with the codebase by choosing issues labeled “good first issue”.

If a contributor decides to start from an issue, we recommend leaving a comment on it to declare that there is a plan to work on that. This way, other contributors can know that someone will address that issue and, in case, decide to join forces and give assistance.

Even if most communication about Mage-OS happens on [Discord](http://chat.mage-os.org/), we encourage contributors to start discussions about specific issues and pull requests on GitHub.

### Code contribution checklist
When submitting a piece of code through a pull request, please follow these recommendations:

- A pull request should have a meaningful title and description. If the PR is a bug fix, it should include a step-by-step guide to reproduce the bug(s). Any additional reasoning (the whys) that justifies the pull request is more than welcome. The more detailed the information is, the more quickly the PR will be processed and the quicker the review process can be completed. Please take the same care writing the PR description as writing the code changes.

- A PR not intended to be merged yet must have either a “[WIP]” prefix in the title or the “wip” label.

- The code should align with the adopted coding standard. At the moment, we can refer to [Adobe Commerce coding stardards](https://developer.adobe.com/commerce/php/coding-standards/). In the future, we would like to automate the process as much as possible with defined rules for static code/architecture analyzers.

- The commit messages should adhere to the [conventional commit standard](https://www.conventionalcommits.org/en/v1.0.0/).

- The commit history should be kept clean, which means the less relevant commits of the same pull request are [squashed](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-commits/squashing-commits). 

- If sufficient tests cover the code, it will significantly speed up the review process. In case of a bug fix, the test should fail because of the defect without the changes introduced by the PR, and the changes make the test pass.

- The PR must not cause other tests to fail. If the failure is because of intended behavioral changes, those tests need to be updated in the same PR, too.

After a PR is submitted, please feel free to add additional review comments to your PR to explain the change to reviewers. Again, this can speed up the review process.

After a PR is submitted, chances are that the review process will require some time; please be patient. The amount of time depends on many factors, but if a contributor feels that the PR is waiting for too long, we recommend trying to contact some maintainers on Discord and point out the situation. To find out a frequent reviewer, just look at other merged PRs.

Be polite and positive in your communication with reviewers. The tone of language can make a big difference.

While waiting for your PR to be reviewed, a contributor may review others’ PRs if they have time, thus freeing the backlog of pending reviews for the maintainers and accelerating the review of their PR.

### Contributor assistant (bot)
>✋ This section describes a feature that's still under discussion and still needs to be developed.

The contributor assistant is a bot that helps automate pull request workflows by using commands entered in comments.

#### Launch new instances

```
// Deploy instance based on PR changes
@mageos give me test instance 


// Deploy vanilla Magento instance based on the specified branch
@mageos give me 2.4-develop instance


// Specific PHP and DB versions
@mageos give me new instance with edition b2b with env php 7.3 database 5.7
```

#### Run tests

```
// Run or re-run all required tests against the PR changes
@mageos run all tests

// Run or re-run specific comma-separated test build(s)
//
// Allowed build names are:
// - Database Compare
// - Functional Tests CE
// - Integration Tests
// - Magento Health Index
// - Sample Data Tests CE
// - Static Tests
// - Unit Tests
// - WebAPI Tests
//
// Please run only needed test builds instead of all when developing.
// Please run all test builds before sending your PR for review. 

// This functionality is limited to Mage-OS maintainers.
@mageos run <test-build(s)>
```

## Code reviews
Every Mage-OS repository contains a `CODEOWNERS` file in the root directory.
The file lists the teams whose members can approve PRs so they may be merged.
At least two reviews by code owners are required before a PR can be merged.

Everybody else may also review PRs, but they can’t fulfill the merge requirements.
Such additional reviews by others are welcome, as they ease the review process for the code owners, and more eyes spot more bugs.

> ✋ Currently, code owner team membership is granted by the Mage-OS board of directors and the technical team lead based on merit. In the future, we will probably formalize a technical steering committee for this task.

When reviewing a pull request, please follow the following guideline:

- Be polite and positive towards the author of the PR in review comments. The tone of language can make a big difference.

- Ensure the PR has a meaningful description. If the PR is a bug fix, the description has to include instructions to reproduce the bug manually. If the PR fixes an issue, ensure the issue is linked to the PR. If the description is lacking, please ask the PR author for clarification. It is okay to ask the author for clarification on a side channel (e.g. Discord) and then add the clarification yourself as a comment to the PR. Or, if you have edit privileges, feel free to improve the description by editing it.

- Once the PR description is sufficient, spend enough time reading the code changes to understand them. This might require reading functionally adjacent code to understand the full context. If the code changes are too hard to understand, please ask the original author to explain or, even better, maybe suggest changes that could make the code more digestible for humans. Generally, the more specific such suggestions are, the better; including examples is good, too.

- Ensure the code doesn’t introduce any backward incompatible changes unless they were previously agreed to by the technical team lead. If so, ask the technical team leads to state their approval in a comment to the PR.

- If the PR is a bug fix, reproduce the bug manually. Then apply the PR changes and confirm the behavior is fixed. If the PR adds a new feature, manually test it works as expected.

- Ensure sufficient tests cover the code and the test suites pass. In case of a bug fix, the tests should fail because of the defect before the changes introduced by the PR, and the changes make the tests pass. If test coverage is not sufficient, either ask the original author to cover the change with tests or - if you have time - offer to write some yourself. Be aware not everyone is familiar with writing tests, which is okay. If necessary, help the PR author with testing, or point them to a resource explaining it.

- Once the PR is functionally complete, check the code aligns with the adopted coding standard. This should be mostly taken care of by the automated GitHub actions. When suggesting changes to the coding style, be aware that these changes are not really important. If you have the time, maybe offer the original author to make those changes for them.

- When the PR is functionally complete and coding standard compliant, check the commit messages and history align with the adopted standard. Fixing the commit history requires re-writing the history, which not everybody is familiar with. Be prepared to help the author by explaining the steps to them or by pointing them to a resource explaining the process.

## Issues
The best way to keep track of bugs is by opening an issue. When creating an issue, please check the following:

- there isn’t another issue addressing the same problem

- the issue can be reproduced, preferably on a fresh install with sample data (ideally on an instance provisioned by the GitHub bot once it is available)

- the issue describes:

    - preconditions and environment
    - steps to reproduce
    - expected result
    - actual result
    - any additional information

Please take the time to provide as much information as possible to help developers understand and reproduce the problem.

Creating an issue does not automatically mean someone will work on it.
The best way an issue is resolved is to create a PR, raise the topic in Discord or the tech meeting, or lobby for support that someone else picks up the issue and fixes it.

The issue on GitHub serves to document the learnings and decisions made along the way and to document progress.
