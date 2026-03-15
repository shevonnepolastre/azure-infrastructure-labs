# Minecraft Azure Quests

A hands-on AZ-104 study environment built around a real-world scenario: running a Minecraft server on Azure. Each quest maps to a core Azure domain and produces working infrastructure — not just notes.

The scenario keeps the work grounded. Every decision (storage for backups, NSGs for access control, VM sizing, DNS) has a practical reason behind it, the same way it would in a production environment.

---

## Why This Exists

Passing AZ-104 requires understanding how Azure services work together, not just what they are individually. This repo documents that process — working through real deployments, hitting real errors, and building the kind of muscle memory that doesn't come from practice exams.

---

## Quest Structure

Each quest folder maps to an AZ-104 domain and contains scenario documentation, deployment files, and notes on what was learned.

| Quest | Domain | What It Covers |
|-------|--------|----------------|
| `01-identities-governance` | Identity & Governance | RBAC, resource locks, access control |
| `02-storage` | Storage | Azure Storage accounts, blob containers, world file backups via AzCopy |
| `03-compute-vm` | Compute | VM deployment, sizing, Minecraft server installation |
| `04-virtual-networking` | Networking | VNets, NSGs, private DNS zones, custom domains |
| `07-bonusquests/vm-automation-stop-start` | Automation | Scheduled VM start/stop to control costs |
| `monitor` | Monitoring | Azure Monitor, alerts, observability basics |

---

## Repository Structure

```
minecraft-azure-quests/
├── .github/
│   └── workflows/
│       ├── deploy.yml                  # CI/CD pipeline for infrastructure deployment
│       └── deploy-storage-account.yml  # Dedicated workflow for storage account deployment
├── quests/                             # Quest documentation and deployment files by domain
├── scripts/
│   ├── backup-world.sh                 # Automates Minecraft world backup to Azure Storage
│   ├── install.minecraft.sh            # Installs and configures Minecraft server on Azure VM
│   └── start-minecraft.sh              # Starts the Minecraft server process
├── ci-cd/                              # CI/CD reference files and pipeline configs
├── docs/                               # Supporting documentation
├── minecraft-specifics/                # Minecraft server configuration files
└── resources/                          # Additional reference materials
```

---

## Infrastructure & Tools

| Tool | How It's Used |
|------|--------------|
| Azure Bicep | Infrastructure as code for all deployments |
| PowerShell (Az module) | Resource management and automation |
| Bash | Server installation and backup scripts |
| GitHub Actions | CI/CD pipelines for automated deployment |
| Azure Storage + AzCopy | World file backups |
| Azure Monitor | Alerts and observability |
| VS Code | Development environment |

---

## CI/CD

Two GitHub Actions workflows handle automated deployment:

- `deploy.yml` — triggers on push to main, deploys core infrastructure via Bicep
- `deploy-storage-account.yml` — dedicated pipeline for storage account provisioning

This mirrors how infrastructure changes are managed in a real team environment: changes go through version control, pipelines validate and deploy, manual portal clicks are the exception not the rule.

---

## Scripts

Three shell scripts handle server lifecycle on the Azure VM:

- `install.minecraft.sh` — installs Java, downloads the Minecraft server binary, and configures the service
- `start-minecraft.sh` — starts the server process
- `backup-world.sh` — copies the world directory to Azure Blob Storage using AzCopy

---

## AZ-104 Domains Covered

- Manage Azure identities and governance
- Implement and manage storage
- Deploy and manage Azure compute resources
- Configure and manage virtual networking
- Monitor and maintain Azure resources

---

## Related Projects

This repo is part of a broader Azure portfolio:

- [Azure Hub-Spoke Network Platform](https://github.com/shevonnepolastre/azure-hub-spoke-platform) — enterprise-grade hub-and-spoke architecture in Bicep
- [Intune Assistant Chatbot](https://github.com/shevonnepolastre/intune-assistant-chatbot) — RAG-based chatbot using Azure AI Foundry and Azure Cognitive Search
