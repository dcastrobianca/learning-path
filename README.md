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
6. **Every week README ends with an "On repeat" section** that lists every command of the week. I check it by rebuilding the setup from the notes alone.

Application code is not the focus of this repository. For the practice application I generate a small Spring Boot service with AI and review it myself, so my time goes into running, securing and fixing it.

Theory (system design and software architecture) and German language study run alongside this, outside the repository.

## Roadmap (about six months)

| Phase | Weeks | Dates | Hands-on focus | Status |
|---|---|---|---|---|
| 1. Foundations | 1-7 | Oct 19 - Dec 6 | Linux VM and manual deployment of a small Spring Boot app with PostgreSQL (3 weeks), Azure basics, Terraform, Docker, GitHub Actions | In progress |
| 2. Kubernetes | 8-15 | Dec 7 - Jan 31 | Local Kubernetes, then AKS provisioned with Terraform and deployed from CI (two holiday weeks at half load) | Planned |
| 3. Platform | 16-23 | Feb 1 - Mar 28 | Helm, Argo CD, dev and staging environments, observability, a multi-tenant Spring Boot service on the platform | Planned |
| 4. Hardening and documentation | 24-27 | Mar 29 - Apr 25 | Secrets management, cost cleanup, architecture documentation, project walkthrough | Planned |

The detailed plan is re-planned weekly, so this table shows direction rather than a fixed schedule. For example, the Linux VM work grew from one week to three when I decided to practice with a realistic application (a database, an API key and an external service) instead of a hello-world, and everything after it moved one week later.

## Repository structure

```
.
├── README.md                  This file
├── week-01-linux-vm/
│   ├── README.md              Weekly summary: goal, outcome, lessons learned, "On repeat"
│   ├── day-01-ubuntu-vm.md    One log per session
│   ├── day-01/                Screenshots and files for that session
│   ├── day-02-ssh-key.md
│   ├── day-02/
│   └── ...
├── week-02-.../
└── ...
```

Conventions:

- One folder per week, named `week-NN-topic`.
- One log file per session, named `day-NN-topic.md`, with a matching `day-NN/` folder for its screenshots and small files.
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

Used so far: Ubuntu Server, VirtualBox, netplan, apt, SSH, systemd and journalctl, nginx.

Planned: PostgreSQL, Spring Boot, Azure, Terraform, Docker, Docker Compose, GitHub Actions, Kubernetes (local and AKS), Helm, Argo CD.

A tool moves to the first list when it appears in a committed session, not before.

## Progress

| Week | Theme | Status |
|---|---|---|
| 1 | Linux VM: build, secure, run a web server, break and fix it | Done |
| 2 | Linux VM, part 2: PostgreSQL, a small Spring Boot app, run as a systemd service | In progress |
| 3 | Linux VM, part 3: nginx reverse proxy, firewall, backup and restore, failure drills | Planned |

## About

Based in Nuremberg, Germany. Backend engineer by background, now building depth in cloud and platform engineering.

- LinkedIn: [linkedin.com/in/dcastrobianca](https://www.linkedin.com/in/dcastrobianca/)
