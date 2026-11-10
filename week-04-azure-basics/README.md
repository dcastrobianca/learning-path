# Week 4: Azure basics, account, budget and resource hierarchy

**Dates:** Nov 9 - Nov 13, 2026 (sessions on Tue, Wed and Thu)
**Status:** In progress

## Goal

Set up the Azure foundation that every later stage builds on: a subscription with a spending alert, a resource group, and a clear picture of where things sit in the Azure hierarchy (management group, subscription, resource group, resource). By Thursday I can show, using my own resources, which level a budget and a role assignment apply to and what each one inherits.

I set the budget before creating anything that costs money. No virtual machine is created this week.

There are no sessions on Monday and Friday this week, so this week has three sessions instead of five. The work that would have filled the rest moves forward:

- Week 5: create a VM in the Azure portal and deploy the expense app on it, using what I built on the local VM in weeks 1-3.
- Week 6: repeat the VM setup with the Azure CLI, then with a first Terraform configuration.

This is the first step from running things on my own machine to running them in the cloud. The expense app from weeks 2 and 3 is not touched this week.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Cloud | Azure subscription (free tier), used through the Azure portal |
| Local VM | The Ubuntu Server VM from weeks 1-3 stays off this week |
| New this week | Azure subscription, Cost Management budgets and alerts, resource groups and tags, role assignment scope |

## Daily plan

Each session is 55 minutes: 10 minutes of foundation reading, 10 minutes of concept check, 25 minutes of hands-on work and 10 minutes of documentation, ending with a commit.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Tue | An Azure subscription I can sign in to, with a monthly budget that emails me before I overspend | I sign in to the portal and see my subscription; a monthly budget exists on the subscription with alerts at 80% and 100%; the alert emails go to my address | Planned | `day-16-azure-account-budget.md` |
| Wed | A tagged resource group created in the portal | A resource group exists in a region I chose; it has at least one tag; I find it and its tag in the portal | Planned | `day-17-azure-resource-group.md` |
| Thu | Every level of the hierarchy located for my own resources, with the level of a budget and of a role assignment identified | I show the resource group, its subscription and the management group above it; I state which level a budget and a role assignment apply to and what each inherits; three open questions are written down | Planned | `day-18-azure-hierarchy.md` |

Foundation reading, each done inside its session:

| Day | Reading |
|---|---|
| Tue | Microsoft Learn, "Tutorial: Create and manage budgets" |
| Wed | Microsoft Learn, "What is Azure Resource Manager?" |
| Thu | Microsoft Learn, "Understand scope for Azure RBAC" |

## Demo

_To fill on Thursday: three screenshots, each with one line on what it proves._

1. The budget on the subscription with its 80% and 100% alerts
2. The resource group with its tag
3. The hierarchy for my own resources, from management group down to resource group

## What I learned

_To fill on Thursday._

- Key concepts:
    * 
- Portal paths I now know without looking them up:
    * 
- What I got wrong first:
    * 
- Three questions I cannot answer yet about the hierarchy:
    1. 
    2. 
    3. 

## On repeat

Portal steps instead of commands this week. I fill in the exact menu path as I go, and I check the list by repeating it in a second, empty resource group.

1. Sign in to the Azure portal and find the subscription

    _menu path:_

2. Create a monthly budget on the subscription

    _menu path:_

3. Add alerts at 80% and 100% of the budget and set the alert email address

    _menu path:_

4. Create a resource group in a chosen region

    _menu path:_

5. Add a tag to the resource group

    _menu path:_

6. Find the subscription and the management group above a resource group

    _menu path:_

7. Find where a role assignment is made at resource group level and at subscription level (view only)

    _menu path:_

## Weekly review

- Planned outcomes met: _pending_ of 3.
- What to change next week:
    * _pending_
