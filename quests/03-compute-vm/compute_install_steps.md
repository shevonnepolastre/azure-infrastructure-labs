# Compute: Minecraft Server Setup on Azure

## Overview

Documenting the steps to deploy and configure a Minecraft server on an Azure VM —
including issues hit along the way and how they were resolved.

---

## Prerequisites

Before provisioning, add your Azure credentials and Linux VM password as GitHub Secrets.
[Guide here](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/docs/add-azure-secret-to-github.md).

---

## Step 1: Provision the VM

Deployed via [Bicep](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/infrastructure/compute.bicep)
and [GitHub Actions](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/yaml-files/deploy-linux-vm.md).

| Setting | Value |
|---------|-------|
| Image | Ubuntu 22.04 LTS |
| Size | Standard B2s (2 vCPU, 4 GB RAM) |
| Region | East US |
| Authentication | SSH Public Key |
| Ports | 22 (SSH), 25565 (Java), 19132 (Bedrock) |

---

## Step 2: Install Java

SSH into the VM after provisioning and install Java.
[Steps documented here](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/docs/updating%20to%20java%2021%20sdk.md).

---

## Step 3: Install the Minecraft Server

Download the server `.jar` file:

```bash
wget [Minecraft jar link]
```

Accept the EULA. Azure has two separate login contexts — your Azure account and the VM admin account.
Had to resolve a login conflict before this would work. Used the VM admin account to run:

```bash
echo "eula=true" > eula.txt
```

Or edit it manually:

```bash
nano eula.txt
```

---

## Step 4: Launch the Server

Standard launch:

```bash
java -Xmx1024M -Xms1024M -jar server.jar nogui
```

If using Fabric (required for mods and shader packs):

```bash
java -Xmx2G -Xms1G -jar fabric-server-launch.jar nogui
```

The server and client use the same launch pattern — different profiles on the client side
map to different server configurations on the server side.

---

## Step 5: Install Fabric or OptiFine for Mods and Shaders

[Details here](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/docs/installing-shader-packs.md).

---

## Step 6: Install Geyser for Bedrock Cross-Play

[Guide here](https://github.com/shevonnepolastre/minecraft-azure-lab/blob/main/docs/bedrock-support.md).

Used the Fabric mod version rather than the standalone. The standalone works but requires
restarting Geyser separately after every VM restart, and it needs its own terminal session.
The Fabric mod handles everything in a single launch — cleaner operationally.
