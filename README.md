# Learning Path: Cloud, DevOps and Platform Engineering

A public, day-by-day record of how I move from using cloud and DevOps tools to building the environments they run on: Linux servers, Azure, containers, Kubernetes, CI/CD and GitOps.

Every working session ends with a commit that documents what I built, what broke and how I fixed it.

## Why this repository exists

I am a Senior Software Engineer with a backend background (Java, Spring, PostgreSQL, MySQL) and I lead a DevOps and Cloud capability team at an automotive software company. In that role I work with Azure, GitHub Actions, Docker, Kubernetes and GitOps tooling as a user. I have not built these environments from scratch, and I want to close that gap deliberately.

Reading about infrastructure does not give me the habits I want: reproducing a setup from my own notes, reading logs under pressure, and fixing what I broke. So I practice in small, measurable steps and keep the evidence here.

This repository is:

- a **learning log**: honest notes, including failures and dead ends
- a **portfolio**: working configurations and documentation I can walk through in a conversation
- a **habit tracker**: the commit history shows consistency over six months

## How I work

The method follows a simple weekly cycle.

1. **Sunday: plan.** I define a specific, testable outcome for each weekday (what I will build or deploy) and a "done when" check that is either true or false.
2. **Each weekday: one session.** 40 minutes of hands-on work, then 10 minutes of documentation: what I deployed, what worked, what did not, and how I solved it.
3. **Every session ends with a commit** to this repository.
4. **Fridays include deliberate debugging.** I break something on purpose and fix it, to build troubleshooting muscle memory.
5. **Sunday: review.** I compare plan and reality, then adjust the next week.

Theory (system design and software architecture) and German language study run alongside this, outside the repository.

## Roadmap (about six months)

| Phase | Weeks | Hands-on focus | Status |
|---|---|---|---|
| 1. Foundations | 1-6 | Linux VM, manual deployment, Azure basics, Terraform, Docker, GitHub Actions | In progress |
| 2. Kubernetes | 7-14 | Local Kubernetes, then AKS provisioned with Terraform and deployed from CI | Planned |
| 3. Platform | 15-22 | Helm, Argo CD, dev and staging environments, observability, a multi-tenant Spring Boot service on the platform | Planned |
| 4. Hardening and documentation | 23-26 | Secrets management, cost cleanup, architecture documentation, project walkthrough | Planned |

The detailed plan is re-planned weekly, so this table shows direction rather than a fixed schedule.

## Repository structure

```
.
├── README.md                  This file
├── week-01-linux-vm/
│   ├── README.md              Weekly summary: goal, outcome, lessons learned
│   ├── day-01-ubuntu-vm.md    One log per session
│   ├── day-02-ssh-keys.md
│   └── ...
├── week-02-.../
└── ...
```

Conventions:

- One folder per week, named `week-NN-topic`.
- One log file per session, named `day-NN-topic.md`.
- Configuration files, scripts and Terraform code live next to the log that introduced them, and move into a dedicated folder once a project outgrows a single week.
- No secrets, keys or credentials are ever committed.

## Session log format

Every `day-NN-*.md` file uses the same structure:

```markdown
# Day NN: <topic>

**Outcome:** what I planned to build or deploy
**Done when:** the check that proves it works

## What I did
Commands and configuration, in order.

## What worked

## What did not work

## How I solved it

## What I would do differently
```

## Tools and technologies

Linux (Ubuntu Server), SSH, nginx, VirtualBox, Azure, Terraform, Docker, Docker Compose, GitHub Actions, Kubernetes (local and AKS), Helm, Argo CD, Spring Boot, PostgreSQL.

Tools are added to this list when they appear in a committed session, not before.

## Progress

| Week | Theme | Status |
|---|---|---|
| 1 | Linux VM: build, secure, run a web server, break and fix it | Done |


## About

Based in Nuremberg, Germany. Backend engineer by background, now building depth in cloud and platform engineering.

- LinkedIn: www.linkedin.com/in/dcastrobianca/
- Contact: biancardc24@gmail.com