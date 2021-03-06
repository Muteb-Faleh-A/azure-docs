---
title: Set up the source environment for disaster recovery of VMware VMs to Azure with Azure Site Recovery | Microsoft Docs'
description: This article describes how to set up your on-premises environment for disaster recovery of VMware VMs to Azure with Azure Site Recovery.
services: site-recovery
author: Rajeswari-Mamilla
manager: rochakm
ms.service: site-recovery
ms.topic: article
ms.date: 10/29/2018
ms.author: ramamill

---

# Set up the source environment for disaster recovery of VMware VMs to Azure

This article describes how to set up your source on-premises environment, to replicate VMware VMs to Azure. It includes steps for selecting your replication scenario, setting up an on-premises machine as the Site Recovery configuration server, and automatically discovering on-premises VMs. 

## Prerequisites

The article assumes that you have already:

- Planned your deployment with the help of [Azure Site Recovery Deployment Planner](site-recovery-deployment-planner.md). This helps you to allocate sufficient bandwidth, based on your daily data-change rate, to meet your desired recovery point objective (RPO).
- [Set up resources](tutorial-prepare-azure.md) in the [Azure portal](http://portal.azure.com).
- [Set up on-premises VMware](vmware-azure-tutorial-prepare-on-premises.md), including a dedicated account for automatic discovery.

## Choose your protection goals

1. In **Recovery Services vaults**, select the vault name. We're using **ContosoVMVault** for this scenario.
2. In **Getting Started**, select Site Recovery. Then select **Prepare Infrastructure**.
3. In **Protection goal** > **Where are your machines located**, select **On-premises**.
4. In **Where do you want to replicate your machines**, select **To Azure**.
5. In **Are your machines virtualized**, select **Yes, with VMware vSphere Hypervisor**. Then select **OK**.

## Set up the configuration server

You can set up the configuration server as an on-premises VMware VM through an Open Virtualization Application (OVA) template. [Learn more](concepts-vmware-to-azure-architecture.md) about the components that will be installed on the VMware VM.

1. Learn about the [prerequisites](vmware-azure-deploy-configuration-server.md#prerequisites) for configuration server deployment.
2. [Check capacity numbers](vmware-azure-deploy-configuration-server.md#capacity-planning) for deployment.
3. [Download](vmware-azure-deploy-configuration-server.md#download-the-template) and [import](vmware-azure-deploy-configuration-server.md#import-the-template-in-vmware) the OVA template to set up an on-premises VMware VM that runs the configuration server. The licence provided with the template is an evaluation licence and is valid for 180 days. Post this period, customer needs to activate the windows with a procured licence.
4. Turn on the VMware VM, and [register it](vmware-azure-deploy-configuration-server.md#register-the-configuration-server-with-azure-site-recovery-services) in the Recovery Services vault.

## Azure Site Recovery folder exclusions from Antivirus program

### If Antivirus software is active on Source machine

If source machine has an Antivirus software active, installation folder should be excluded. So, exclude folder *C:\ProgramData\ASR\agent* for smooth replication.

### If Antivirus Software is active on Configuration server

Exclude following folders from Antivirus software for smooth replication and to avoid connectivity issues

 1. C:\Program Files\Microsoft Azure Recovery Services Agent.
 2. C:\Program Files\Microsoft Azure Site Recovery Provider
 3. C:\Program Files\Microsoft Azure Site Recovery Configuration Manager 
 4. C:\Program Files\Microsoft Azure Site Recovery Error Collection Tool 
 5. C:\thirdparty
 6. C:\Temp
 7. C:\strawberry
 8. C:\ProgramData\MySQL
 9. C:\Program Files (x86)\MySQL
 10. C:\ProgramData\ASR
 11. C:\ProgramData\Microsoft Azure Site Recovery
 12. C:\ProgramData\ASRLogs
 13. C:\ProgramData\ASRSetupLogs
 14. C:\ProgramData\LogUploadServiceLogs
 15. C:\inetpub
 16. ASR server installation directory. For example: E:\Program Files (x86)\Microsoft Azure Site Recovery

### If Antivirus Software is active on scale-out Process server/Master Target

Exclude following folders from Antivirus software

1. C:\Program Files\Microsoft Azure Recovery Services Agent
2. C:\ProgramData\ASR
3. C:\ProgramData\ASRLogs
4. C:\ProgramData\ASRSetupLogs
5. C:\ProgramData\LogUploadServiceLogs
6. C:\ProgramData\Microsoft Azure Site Recovery
7. ASR load balanced process server installation directory, Example: C:\Program Files (x86)\Microsoft Azure Site Recovery

## Common issues
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]

## Next steps
[Set up your target environment](./vmware-azure-set-up-target.md) in Azure.
