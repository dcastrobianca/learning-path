# Learning Path: Cloud, DevOps and Platform Engineering

A public, day-by-day record of how I move from using cloud and DevOps tools to building the environments they run on: Linux servers, Azure, containers, Kubernetes, CI/CD and GitOps.

Every working session ends with a commit that documents what I built, what broke and how I fixed it.

## Why this repository exists

I am a Senior Software Engineer with a backend background (Java, Spring, PostgreSQL, MySQL) and I lead a DevOps and Cloud capability team at an automotive software company. In that role I work with Azure, GitHub Actions, Docker, Kubernetes and GitOps tooling as a user. I have not built these environments from scratch, and I want to close that gap deliberately.

Reading about infrastructure does not give me the habits I want: reproducing a setup from my own notes, reading logs under pressure, and fixing what I broke. So I practice in small, measurable steps and keep the evidence here.

This repository is:

- a **learning log**: honest notes, including failures and dead ends
- a **portfolio**: working configurations and documentation I can walk through in a conversation
- a **habit tracker**: the commit history shows consistency over eight months

## How I work

The method follows a simple weekly cycle.

1. **Saturday: plan.** I define a specific, testable outcome for each session (what I will build or deploy) and a "done when" check that is either true or false.
2. **Each session has four parts.** Foundation reading, a short concept check on the key ideas, hands-on work, and documentation: what I deployed, what worked, what did not, and how I solved it. A session takes 55 to 90 minutes, and the reading happens inside it.
3. **Every session ends with a commit** to this repository.
4. **Weeks with something to break end with deliberate debugging.** I break the setup on purpose and fix it, to build troubleshooting muscle memory.
5. **Saturday: review.** I compare plan and reality, then adjust the next week. Some weeks have fewer than five sessions, and the plan moves with my real schedule rather than being squeezed.
6. **Every week's README ends with an "On repeat" section** that lists every command or portal step of the week. I check it by rebuilding the setup from the notes alone.

Application code is not the focus of this repository. For the practice application I generate a small Spring Boot service with AI and review it myself, so my time goes into running, securing and fixing it.

Theory (system design and software architecture) and German language study run alongside this, outside the repository.

## Roadmap (about eight months)

| Phase | Weeks | Dates | Hands-on focus | Status |
|---|---|---|---|---|
| 1. Foundations | 1-9 | Oct 19 - Dec 20 | Linux VM and manual deployment of a small Spring Boot app with PostgreSQL (3 weeks), Azure basics, an Azure VM and the same app on it (weeks 4-5), Azure CLI and Terraform (weeks 6-7), Docker, Docker Compose, a container registry and a GitHub Actions build and push (weeks 8-9) | In progress |
| 2. Data and Kubernetes | 12-21 | Jan 4 - Mar 14 | Kubernetes locally, then AKS provisioned with Terraform, deployment from GitHub Actions, cost review and a full demo (weeks 10-11 are holiday buffer weeks) | Planned |
| 3. Platform | 22-32 | Mar 15 - May 30 | Helm, Argo CD, dev and staging environments, observability, a multi-tenant Spring Boot service on the platform | Planned |
| 4. Hardening and documentation | 33-36 | May 31 - Jun 27 | Secrets management with Key Vault, cost cleanup, architecture documentation, project walkthrough | Planned |

The detailed plan is re-planned weekly, so this table shows direction rather than a fixed schedule. Three examples:

- The Linux VM work grew from one week to three when I decided to practice with a realistic application (a database, an API key and an external service) instead of a hello-world, and everything after it moved one week later.
- Week 4 was planned to end with the first Azure VM on Thursday. That session did not happen, so the VM moved to Wednesday of week 5, and week 5 has three sessions (Wednesday, Thursday and Saturday) instead of five.
- In November I reduced the weekly study time to 1h30 per day and added a Saturday block for review and "on repeat". The plan now ends in June instead of April, and no topic was cut: when I am behind I move the date, not the depth.

## Repository structure

```
.
├── README.md                                    This file
├── week-01-linux-vm/
│   ├── README.md                                Weekly summary: goal, outcome, lessons learned, "On repeat"
│   ├── day-01-ubuntu-vm.md                      One log per session
│   ├── day-01/                                  Screenshots and files for that session
│   ├── day-02-ssh-key.md
│   ├── day-02/
│   └── ...
├── week-02-vm-running-app/
├── week-03-vm-networking-failure-drills/
├── week-04-azure-basics/
├── week-05-azure-vm-expense-app/
└── ...
```

Conventions:

- One folder per week, named `week-NN-topic`.
- One log file per session, named `day-NN-topic.md`, with a matching `day-NN/` folder for its screenshots and small files. Day numbers count sessions, not calendar days, so a week with four sessions uses four numbers.
- Configuration files, scripts and Terraform code live next to the log that introduced them, and move into a dedicated folder once a project outgrows a single week.
- No secrets, keys or credentials are ever committed.

## Session log format

Every `day-NN-*.md` file uses the same structure:

```markdown
# Day NN: <topic>

**Outcome:** what I planned to build or deploy
**Done when:** the check that proves it works

## What I did
Commands, configuration or portal steps, in order.

## What worked

## What did not work

## How I solved it

## What I would do differently
```

## Tools and technologies

Used so far: Ubuntu Server, VirtualBox, netplan, apt, SSH, systemd and journalctl, PostgreSQL, Java and Maven, a Spring Boot service, nginx, ufw, pg_dump and pg_restore, curl, the Azure portal (subscriptions, Cost Management budgets, resource groups, tags, management groups, access control (IAM) in view-only mode).

Planned: Azure (VMs, role assignments, CLI), Terraform, Docker, Docker Compose, GitHub Actions, Kubernetes (local and AKS), Helm, Argo CD.

A tool moves to the first list when it appears in a committed session, not before.

## Progress

| Week | Theme | Status |
|---|---|---|
| 1 | Linux VM part 1: build, secure, run a web server, break and fix it | Done |
| 2 | Linux VM, part 2: PostgreSQL, a small Spring Boot app, run as a systemd service | Done |
| 3 | Linux VM, part 3: nginx reverse proxy, firewall, backup and restore, failure drills | Done |
| 4 | Azure basics: account, budget, resource group, hierarchy (four sessions planned, three done; the first VM moved to week 5) | Done |
| 5 | Azure VM: create it in the portal, run the expense app on it, nginx and a network security group (three sessions) | In progress |

## About

Based in Nuremberg, Germany. Backend engineer by background, now building depth in cloud and platform engineering.

- LinkedIn: [linkedin.com/in/dcastrobianca](https://www.linkedin.com/in/dcastrobianca/)
