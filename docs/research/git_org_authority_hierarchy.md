# How do I setup Github organization with large amount of members?

- [How do I setup Github organization with large amount of members?](#how-do-i-setup-github-organization-with-large-amount-of-members)
  - [Introduction](#introduction)
  - [What is Github Organization?](#what-is-github-organization)
  - [How to setup a Github Organization?](#how-to-setup-a-github-organization)
    - [Initial setup](#initial-setup)
    - [Inviting members](#inviting-members)
    - [Teams](#teams)
      - [Nested teams](#nested-teams)
    - [Roles](#roles)
      - [Organization-level roles](#organization-level-roles)
      - [Team-level roles](#team-level-roles)
      - [Repository-level roles](#repository-level-roles)
  - [How are Github Organizations applicable to real world scenarios?](#how-are-github-organizations-applicable-to-real-world-scenarios)
    - [Company security and attack vectors](#company-security-and-attack-vectors)
      - [Weak credentials](#weak-credentials)
      - [Exposed secret keys](#exposed-secret-keys)
      - [Deprecated and unsupported dependencies](#deprecated-and-unsupported-dependencies)
      - [Social engineering](#social-engineering)
    - [What happens after system has been breached?](#what-happens-after-system-has-been-breached)
  - [What are advantages and disadvantages or Github Organizations?](#what-are-advantages-and-disadvantages-or-github-organizations)
  - [What are possible alternatives to Github Organizations?](#what-are-possible-alternatives-to-github-organizations)
  - [References](#references)


## Introduction

This research paper primarily focus on setting up a new Github Organization with a suitable authority management and role hierarchy structure for fast and secure development.

In this day and age, it isn't uncommon to hear that big software companies are being hacked and their entire codebase or their entire data storage has been erased or leaked. This research won't focus on sole point of defeating of preventing system breach, but how can we mitigate access once the system has been breached.

*This research is done using the DOT framework and utilizing its strategies and methods, predominantly using "Library" and "Workshop" methods.[^1]*

## What is Github Organization?

Github Organization is the easiest way for developers to manage and collaborate across many different projects. Technically speaking, Organization is a shared Github account that serves as a container for projects and gives the collection of projects a name and a brand. 

People that already have a Github personal account are eligible to collaborate on shared projects by joining the the same organization account. Organization members can be given different roles and permissions, and therefore given responsibility within the organization. For example, organization owners have permission to use Github's refined security and supervisory features to manage organization's resources.

## How to setup a Github Organization?

Good start makes all the difference. As Abraham Lincoln once said: "*If I had six hours to chop down a tree, I’d spend the first four hours sharpening the axe.*".

### Initial setup

Creating an organization on Github is straight forward, click on your profile photo and click **Your organizations**. On new loaded page, click on **New organization** button. 

Organization creation page will pop up and if all the steps are followed, your organization should be created.

### Inviting members

As previously, mentioned, Github Organizations are just shared account that holds repositories that its members can contribute to. 

For someone to be able to contribute to project, they need to be invited to join the organization. After someone has been invited to join the organization, they will receive the invitation link in their email inbox. The invitation expires in 7 days if not accepted.[^2]

When accepted, default user role will be set to **organization member**. See more about roles [here](#roles).

### Teams

Let's imagine a scenario where your organization has experienced a dramatic growth. If the organization is growing, company probably has to hire more people to support the customer expansion. Often the number of employees starts to get out of hand in these situations and manual employee management can get cumbersome. That's the time where employee grouping and teaming starts to sound lot more reasonable both on management level and development level, and that's where Github teams come into play.

Github Teams allow you to create teams within the company and invite members to said team. Any permission setting or access setting you set will reflect on each team member. That was you can limit employee capabilities and visibility access based on their position within the company. 

Each team has its own page within an organization. On a team's page, you can view team members, child teams, and the team's repositories. Organization owners and team maintainers can access team settings and update the team's description and profile picture from the team's page.[^3]

#### Nested teams

If for some reason you want to build a hierarchy tree with team, Github allows it with nested teams. You can create multiple teams within a team. That way, you can mention the parent team from any nested team in the organization and all direct and indirect members of mentioned team will receive a notification. Finally, child teams inherit permissions from th parent team. That means, if you grant a parent team write access, this access level applies to **all** other teams in the hierarchy.

```
YourOrg
├─ Employees
│  ├─ Engineers
│  │  ├─ ApplicationEngineering
│  │  ├─ ClientSystems
│  │  ├─ Identity
```
*Source: Example organization structure utilizing nested teams [^4]*

### Roles

> To perform any actions on GitHub, such as creating a pull request in a repository or changing an organization's billing settings, a person must have sufficient access to the relevant account or resource. This access is controlled by permissions. A permission is the ability to perform a specific action. For example, the ability to delete an issue is a permission. A role is a set of permissions you can assign to individuals or teams.[^5]

As per Github's official documentation, roles are groups of permissions that are easy assignable to any organization member or team, and they dictate available actions for said user or team. For example, deleting an issue is a permission which can be part of a role to assigned user or team, and they can't perform that action without being assigned that role.

There are 3 levels of roles:
- Organization-level roles 
- Team-level roles
- Repository-level roles.

#### Organization-level roles

Organization-level roles are roles which can be assigned to individual members or teams of individuals that allows role assignees to manage organizations, repositories, organizations teams ans settings.


#### Team-level roles

Team-level roles are roles which can be assigned to individuals to manage a certain team. One of the possible team roles is **team maintainer**, which gives the role assignee a number of administrative roles over the team.


#### Repository-level roles

Repository-level roles are roles which can be assigned to organization members, outside collaborators and organization teams and their access restrictions can vary widely.

<br>

_See [here](https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#permissions-for-organization-roles) for more detailed breakdown of role permissions._

<br>

## How are Github Organizations applicable to real world scenarios?

In recent years, Github has become a cornerstone in average software developer's workflow. From repository hosting, [managing workflows](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects), [code reviews](https://github.com/features/code-review) to integrated [CI/CD](https://github.com/features/actions) tooling. Every aspect of software developer's workday can be improved/iterated upon using some Github feature, which only speaks of Github's versatility and developer-centric experience.

As previously mentioned, Github Organizations are a great way to structure a company and manage large amount of projects and people working on those projects. But there is one aspect that is often overlooked with having a properly setup organization: **security**. 

### Company security and attack vectors

Security is frequently neglected when setting up Github organizations or repositories, especially if visibility set to private. Possibility of a breach will never be nullified, but can be reduced. Generally, there are few common attack vectors that are being exploited time and time again:

- Weak credentials
- Exposed secret keys
- Deprecated and unsupported dependencies
- Social engineering

#### Weak credentials

Brute forcing a password is a thing of the past, but every now and then passwords or secret key gets brute forced because it's such an easy vector to exploit. Systems that are exploitable and highly susceptible to security breach due to weak credentials pose a large risk to a business owner.

It's really unfortunate and honestly, quite depressing to see any system brute forced in this day and age because it's extremely easy to protect yourself from brute force. Brute force isn't combated by password complexity but length. Long passwords increase the number of breach attempts, more attempts mean more computational power, more computational power means more processor cycles, which in turn means **time**.

The longer the password, the larger time frame for breaching said password. But in this day and age, [most](https://www.theverge.com/2019/4/18/18485599/facebook-instagram-passwords-plain-text-millions-users) passwords are encrypted, which means they are stored in a manner where some sort of algorithm is used to [hash](https://auth0.com/blog/hashing-passwords-one-way-road-to-security/) the password to hide the original password, and in the process to change original password length to some standard length like 40 or 64 characters. 

That said, hashing algorithms are irreversible so that leaves potential attackers scramble to build a list of most common passphrases to try to utilize, which is called a dictionary attack. Common protection against dictionary attacks is password complexity paired with presence of unorthodox characters.

#### Exposed secret keys

Exposing secret keys is one of the rookie mistakes that can put codebase in danger. Usually secret keys are issued by external services for authenticate users or organizations to access the platform's features. Commonly these keys are a strings of randomly chosen characters.

These keys are repeatedly left out in code, either actual codebase, infrastructure configuration files or CI/CD pipeline configuration files. Once they are left, they can be used to access said external services impersonating the user or company.

There is a very simple remedy for leaked exposed keys, and that is **environment variables**. All operating systems allow to have environment variables available. There a numerous ways to set environment variables, like **.env** files, shell scripts that set environment variables, and setting them online for external services like Github Actions.


#### Deprecated and unsupported dependencies

Deprecated and supported dependencies are a simple way to introduce security risks. Old and deprecated libraries and packages are no longer maintained by developers. That means any security vulnerabilities or flaws discovered in these packages will likely remain unaddressed. Without security updates, the codebase becomes more susceptible to exploitation by attackers who can leverage known vulnerabilities to compromise the system.

As time goes on, security flaws in deprecated packages become more widely known, making them attractive targets for attackers. Potential attackers actively search for systems that use outdated packages because they are more likely to find vulnerabilities that have not been patched. By relying on deprecated packages, you expose your codebase to a higher risk of being exploited. You miss out on the advancements in security that newer packages offer, including stronger encryption algorithms, improved input validation, and better protection against common attack vectors.

This can also be combated quite easily by keeping up-to-date with latest security updates by e.g. means of scheduled maintenance. One solution specific to Github is a bot which notifies you of latest security updates and patches called Dependabot[^6].

#### Social engineering

Easiest vector to exploit of all is a human. Social engineering poses a significant risk to codebase security because it exploits human vulnerabilities instead of technical flaws. It can lead to unauthorized access to code and systems by tricking individuals into revealing sensitive information or granting unauthorized privileges. Attackers may use tactics like impersonation, phishing emails, or deceptive websites to steal login credentials or distribute malware.

To mitigate these risks, organizations should prioritize security awareness and training programs, implement multi-factor authentication, enforce strong password policies, and promote a culture of security vigilance.

### What happens after system has been breached?

After attacker has gained access of the victim's system, all aspects of companies intellectual property is exposed for attacks of any kind **if access hasn't been limited in the first place by administration**. If access hasn't been limited, in the first place, the attacker could've gained access of possibly all intellectual property and would have permission to do anything with it. 

## What are advantages and disadvantages or Github Organizations?

Main advantage is supercharged collaboration. Github's user experience has always been the main focus for Github and hopefully it will stay like that for years to come. Some of the other advantages include tidy code and member management, integration ecosystem and resource availability.

Main disadvantage is reliance on external system because if any part of Github's infrastructure crashes or becomes unavailable, whole workflow is impacted. Other main disadvantage in some people's eyes is data and security compliance. Certain companies are oriented at very specific business cases and if they cannot adapt to Github's security and data standard, they are forced to seek another service.

## What are possible alternatives to Github Organizations?

Main competitor to Github is Gitlab. Gitlab offers very similar features to Github along with option of hosting it locally[^7].

Other noteworthy competitor to Github Organizations is Azure DevOps. Recently it has become quite popular for its integration with anything made by Microsoft. It scales outstandingly good for something made by Microsoft and developers have grown to like it very much.

Last noteworthy competitor to Github Organizations is Jira Software. Although some may argue they serve different purposes, this research focuses on team collaboration and management. They both do it really well, but Jira offers more opportunities for more enterprise-oriented companies more than Github. It's focused on collaboration of all sorts, while Github's main focus is software development. Both have their pros and cons and ultimately shine in different use cases.
<br>

## References

[^1]: https://ictresearchmethods.nl/The_DOT_Framework
[^2]: https://docs.github.com/en/organizations/managing-membership-in-your-organization/inviting-users-to-join-your-organization#about-organization-invitations
[^3]: https://docs.github.com/en/organizations/organizing-members-into-teams/about-teams#team-pages
[^4]: https://nira.com/managing-teams-and-organizations-in-github/
[^5]: https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#about-roles
[^6]: https://github.blog/2020-06-01-keep-all-your-packages-up-to-date-with-dependabot/
[^7]: https://about.gitlab.com/install/


<!-- - what are the alternatives in this field and why use them over this -->