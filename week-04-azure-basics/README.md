# Week 4: Azure basics, account, budget, resource hierarchy and a first VM

**Dates:** Nov 9 - Nov 13, 2026 (sessions on Mon, Tue, Wed and Thu)
**Status:** In progress

## Goal

Set up the Azure foundation that every later stage builds on: a subscription with a spending alert, a resource group, a clear picture of where things sit in the Azure hierarchy (management group, subscription, resource group, resource), and a first Linux VM that I can reach over SSH. By Wednesday I can show, using my own resources, which level a budget and a role assignment apply to and what each one inherits. By Thursday the VM exists, I can connect to it, and it is stopped so that it does not use my free credit.

I set the budget before creating anything that costs money. The VM is the only resource this week that can cost money, and it is created on the last day, after the budgets are in place.

There is no session on Friday this week, so this week has four sessions instead of five. The two long sessions (Wednesday and Thursday, 90 minutes each) pull work forward from week 5:

- Week 5: deploy the expense app on the VM I create this week, and write down what differs from the local VM.
- Week 6: repeat the VM setup with the Azure CLI, then with a first Terraform configuration.

This is the first step from running things on my own machine to running them in the cloud. The expense app from weeks 2 and 3 is not touched this week.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Cloud | Azure subscription (free tier), used through the Azure portal |
| Region | North Europe: among the cheaper European regions and close to Nuremberg |
| Local VM | The Ubuntu Server VM from weeks 1-3 stays off this week |
| New this week | Azure subscription, Cost Management budgets and alerts, resource groups and tags, role assignment scope, a Linux VM in Azure with SSH key login and auto-shutdown |

## Daily plan

Mon and Tue are 55 minutes each: 10 minutes of foundation reading, 10 minutes of concept check, 25 minutes of hands-on work and 10 minutes of documentation. Wed and Thu are 90 minutes each: 15 minutes of foundation reading, 10 minutes of concept check, 55 minutes of hands-on work and 10 minutes of documentation. Every session ends with a commit.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Mon | An Azure subscription I can sign in to, with a monthly budget that emails me before I overspend | I sign in to the portal and see my subscription; a monthly budget exists on the subscription with alerts at 80% and 100%; the alert emails go to my address | Done | `day-16-azure-account-budget.md` |
| Tue | A tagged resource group created in the portal | A resource group exists in a region I chose; it has at least one tag; I find it and its tag in the portal | Done | `day-17-azure-resource-group.md` |
| Wed | Every level of the hierarchy located for my own resources, where a role assignment is made identified, and a budget on the resource group | I show the resource group, its subscription and the management group above it; I show where a role assignment is made at both levels and which of my access is inherited; a budget exists on the resource group only, with an alert at 100%; three open questions are written down | Planned | `day-18-azure-hierarchy.md` |
| Thu | A Linux VM in my resource group that I can reach over SSH from Windows, then stopped so it does not use my credit | The VM exists in my resource group with SSH key login; I connect from Windows and run `hostnamectl`; I name every resource created alongside the VM; the VM is stopped (deallocated) and auto-shutdown is set | Planned | `day-19-azure-linux-vm.md` |

Foundation reading, each done inside its session:

| Day | Reading |
|---|---|
| Mon | Microsoft Learn, "Tutorial: Create and manage budgets" |
| Tue | Microsoft Learn, "What is Azure Resource Manager?" |
| Wed | Microsoft Learn, "Understand scope for Azure RBAC" |
| Thu | Microsoft Learn, "Quickstart: Create a Linux virtual machine in the Azure portal" |

## Demo

_To fill on Thursday: four screenshots, each with one line on what it proves._

1. The budget on the subscription with its 80% and 100% alerts
2. The resource group with its tag, in North Europe
3. The hierarchy for my own resources, from management group down to resource group, and the budget on the resource group
4. The VM connected over SSH from Windows, and the same VM shown as stopped (deallocated) in the portal

## What I learned

_To fill on Thursday._

- Key concepts:
    * Azure scope:
        * Management group: subscriptions, and other management groups.
        * Subscription: resource groups, and the billing relationship.
        * Resource group: resources that share a lifecycle.
        * Resource: one instance of a service, such as a VM or a storage account.
- Portal paths I now know without looking them up:
    * 
- What I got wrong first:
    * 
- Three questions I cannot answer yet about the hierarchy:
    1. 
    2. 
    3. 

## On repeat

Portal steps instead of commands this week. I check the list by repeating it in a second, empty resource group.

1. Sign in to the Azure portal and find the subscription

    _menu path:_ All resources > Organization > Subscriptions

2. Create a monthly budget on the subscription

    _menu path:_ my subscription > Cost Management > Budgets > Add

3. Add alerts at 80% and 100% of the budget and set the alert email address

    _menu path:_ in the same wizard, Next > Set alerts

4. Create a resource group in a chosen region, with a tag

    _menu path:_ All resources > Resource groups > Create, then Next > Tags

5. Check the resource group and its tag

    _menu path:_ All resources > Resource groups, and All resources > Tags

6. Find the subscription and the management group above a resource group

    _menu path:_

7. Find where a role assignment is made at resource group level and at subscription level (view only), and see which access is inherited

    _menu path:_

8. Create a budget on the resource group only, with an alert at 100%

    _menu path:_

9. Create a Linux VM in the resource group with SSH key login and inbound SSH only

    _menu path:_

10. Connect to the VM over SSH from Windows

    _command:_

11. List the resources created alongside the VM

    _menu path:_

12. Set auto-shutdown and stop the VM so that it is deallocated

    _menu path:_

## Weekly review

- Planned outcomes met: _pending_ of 4.
- What to change next week:
    * _pending_
