# Acceptance criteria for community contributions

This document outlines the criteria and process for accepting new modules and code contributions
into the Mage-OS ecosystem, utilizing GitHub Discussions for submissions, voting, and decision-making.

[TOC]

## Acceptance Criteria for a module in mage-os-lab

### Requirements

**Value and Functionality**
* Provides significant value to a meaningful portion of Mage-OS users (either in require or require-dev)
* Offers unique functionality not already available in core Mage-OS
* Or demonstrably improves performance, security, or usability of existing features
* Solves a clear problem or fills a gap in the ecosystem

**Technical Requirements**
* Maintains high code quality with proper patterns and practices
* Follows Mage-OS/Magento coding standards
* Demonstrates compatibility with latest Mage-OS version
* Demonstrates active maintenance (recent updates, responsive to issues)
* Implements security best practices with no known vulnerabilities
* Avoids introducing excessive dependencies
* Follows semantic versioning principles

**Documentation and Support**
* Contains comprehensive documentation (usage, configuration, troubleshooting)
* Includes clear installation instructions
* Show evidence of community adoption and support

**Licensing and Compliance**
* Uses a compatible open-source license: OSL3, BSD3, MIT, AFL (code released under GPL cannot be accepted)
* Complies with all legal requirements
* Contains proper attribution for any third-party code or dependencies

### Submission Process

1. **Create Module**: Develop your module following Mage-OS standards and best practices
2. **Submit Proposal**: Create a new discussion in the designated GitHub repository (TBD) using the "Module Submission" category
3. **Complete Template**: Fill out the provided submission template with details about:
    * Purpose and functionality
    * Target audience/users
    * Technical implementation overview
    * Testing approach
    * Dependencies
    * Maintenance plan
    * Repository link where the module code can be reviewed

### Evaluation Process

#### 1. Community Review (15 Days)

* All module submissions will be open for community review for 15 calendar days starting from the next technical meeting
* Community members can provide feedback through:
    * GitHub Discussion comments for technical feedback
    * GitHub Discussion up/down votes for simple voting

#### 2. Technical Board Assessment

* After the community review period, the Technical Board will assess the module based on:
* Community feedback and votes
* Compliance with acceptance criteria
* Strategic alignment with Mage-OS roadmap
* Long-term maintainability

#### 3. Decision Communication

* The final decision will be communicated in the Discussion thread with explanation
* Possible outcomes include:
* Accept: Module approved for inclusion in mage-os-lab namespace
* Revise: Module requires specific changes before acceptance
* Reject: Module not accepted with explanation

#### 4. Revision Process

When a "Revise" decision is made:
* The Technical Board will provide specific, actionable feedback on required changes
* The module submitter has 30 days to implement requested changes
* Once changes are complete, the submitter adds a comment in the original Discussion thread indicating completion and linking to the updated code
* The Technical Board will conduct a focused re-evaluation within 15 days
* After re-evaluation, a final decision of "Accept" or "Reject" will be made
* In special cases, a second revision round may be granted at the Technical Board's discretion

### Post-Acceptance Requirements

Accepted modules must maintain:
* Timely responses to bug reports and security issues
* Compatibility with new Mage-OS releases
* Adherence to semantic versioning
* Documentation updates when functionality changes

## Deprecation and Removal

Modules may be marked for deprecation and eventual removal if:
* No active maintenance for an extended period
* Critical issues remain unaddressed
* Incompatibility with current Mage-OS versions
* Functionality has been superseded by core features


## Migration from mage-os-lab to mage-os

### Migration Criteria

The module must:
* comply to the same criterias for general admission
* demonstrate proven value and stability through real-world usage and community adoption.
* be actively maintained, with recent updates and responsiveness to issues.
* not have unresolved critical bugs or security vulnerabilities.

### Migration Process

1. Initiation
    * Submit a migration request via a designated GitHub Discussion or issue in the relevant repository.
    * Provide evidence of adoption, maintenance, and compliance with Mage-OS standards.
2. Community Review
    * Open a 15-day review window for community feedback and voting, similar to new module submissions.
3. Technical Board Assessment
    * The Technical Board reviews feedback and ensures all criteria are met.
    * Special attention is given to long-term maintainability, strategic fit, and compatibility with Mage-OS core.
4. Decision
    * The outcome (approve, request changes, or reject) is communicated in the original thread.
    * If changes are requested, a 30-day window is given for revisions, followed by a focused re-evaluation.


## Bundling a Module into the Official Mage-OS Release

### Bundling Criteria

* The module must address a core need for a significant portion of Mage-OS users.
* It should not duplicate functionality already in the core or another bundled module.
* The module must be stable, well-maintained, and fully compatible with the latest Mage-OS release.
* Code quality, documentation, and security must meet the highest standards.
* License must be compatible with Mage-OS requirements.

### Bundling Process

1. Proposal
    * Submit a bundling proposal via GitHub Discussion or issue, outlining the case for inclusion (user impact, necessity, maintenance plan).
2. Community Review
    * Open a 15-day period for community input and voting, mirroring the module acceptance process.
3. Technical Board Review
    * The Technical Board evaluates the proposal, considering community feedback, technical merit, and strategic alignment.
4. Decision
    * The final decision (accept, request changes, or reject) is posted with rationale.
    * If changes are required, a revision window is provided, followed by a re-evaluation.

## Abandoned community projects

If a project is in the mage-os-lab namespace, didn’t reach a stable release, and becomes inactive for an
extended period, it will be archived.

Before archival an admin will modify the project’s README file adding this notice at the beginning:

```
### ⚠️ Project Archived
This Mage-OS project did not reach a stable release and has been inactive for an extended period.
Archiving is not permanent, if you’d like to resume development, contact the Mage-OS maintainers to have it unarchived.
🧡 Thank you to all who contributed.

----
```
