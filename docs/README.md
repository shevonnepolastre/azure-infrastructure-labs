# Azure Infrastructure Labs 

An AZ-104 study lab built around a real scenario: deploying and managing a Minecraft server on Azure. Every quest maps to an exam domain and produces working infrastructure. The scenario is just a framing device — the Azure work is real.

---

## Why I Built It This Way

I learn by doing, not by reading. The fastest way for me to internalize how Azure services connect is to deploy something that actually breaks when I misconfigure it. Choosing a Minecraft server gave every decision a concrete reason: storage for world file backups, NSGs to control who can connect, VM sizing that balances cost and performance, DNS so the server has a usable address. The same thinking applies in production environments. The scenario just makes it easier to stay engaged.

---

## Quest Structure

Each quest folder maps to an AZ-104 exam domain and contains scenario documentation, deployment files, and notes on what I learned — including what broke and why.

| Quest | Domain | What It Covers |
|-------|--------|----------------|
| `01-identities-governance` | Identity & Governance | RBAC, resource locks, access control |
| `02-storage` | Storage | Storage accounts, blob containers, world file backups via AzCopy |
| `03-compute-vm` | Compute | VM deployment, sizing, Minecraft server installation |
| `04-virtual-networking` | Networking | VNets, NSGs, private DNS zones, custom domains |
| `07-bonusquests/vm-automation-stop-start` | Automation | Scheduled VM start/stop for cost control |
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

## Infrastructure and Tools

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

Infrastructure changes go through version control. The pipeline validates and deploys. Manual portal clicks are the exception.

---

## Scripts

Three shell scripts handle server lifecycle on the Azure VM:

- `install.minecraft.sh` — installs Java, downloads the server binary, configures the service
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

- [Azure Hub-Spoke Network Platform](https://github.com/shevonnepolastre/azure-hub-spoke-platform) — enterprise hub-and-spoke architecture built in Bicep
- [Intune Assistant Chatbot](https://github.com/shevonnepolastre/intune-assistant-chatbot) — RAG-based chatbot using Azure AI Foundry and Azure Cognitive Search
