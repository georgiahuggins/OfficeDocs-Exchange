﻿---
title: 'Exchange 2013 virtualization: Exchange 2013 Help'
TOCTitle: Exchange 2013 virtualization
ms:assetid: 36184b2f-4cd9-48f8-b100-867fe4c6b579
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ619301(v=EXCHG.150)
ms:contentKeyID: 49289229
ms.date: 08/08/2017
mtps_version: v=EXCHG.150
---

# Exchange 2013 virtualization

 

_**Applies to:** Exchange Server 2013_


You can deploy Microsoft Exchange Server 2013 in a virtualized environment. This topic provides an overview of the scenarios that are supported for deploying Exchange 2013 on hardware virtualization software.

**Contents**

Requirements for hardware virtualization

Host machine storage requirements

Exchange storage requirements

Exchange memory requirements and recommendations

Host-based failover clustering and migration for Exchange

The following terms are used in this discussion of Exchange virtualization:

  - **Cold boot**   When bringing a system from a power-off state into a clean start of the operating system, the action is a *cold boot*. No operating system state has been persisted in this case.

  - **Saved state**   When a virtual machine is powered off, hypervisors typically have the ability to save the state of the virtual machine, so when the machine is powered back on, it returns to that *saved state* rather than going through a cold boot startup.

  - **Planned migration**   When a system administrator initiates the move of a virtual machine from one hypervisor host to another, the action is a *planned migration*. The action could be a single migration, or a system administrator could configure automation to move the virtual machine on a timed basis. A planned migration could also be the result of some other event that occurs in the system, other than hardware or software failure. The key point is the Exchange virtual machine is operating normally and needs to be relocated for some reason. This relocation can be done via technology, like Live Migration or vMotion. However, if the Exchange virtual machine or the hypervisor host where the virtual machine is located experiences some sort of failure condition, the outcome isn't characterized as a planned migration.

## Requirements for hardware virtualization

Microsoft supports Exchange 2013 in production on hardware virtualization software only when all the following conditions are true:

  - The hardware virtualization software is running one of the following:
    
      - Any version of Windows Server with Hyper-V technology or Microsoft Hyper-V Server
    
      - Any third-party hypervisor that has been validated under the [Windows Server Virtualization Validation Program](https://go.microsoft.com/fwlink/p/?linkid=125375).
    

    > [!NOTE]
    > Deployment of Exchange 2013 on Infrastructure-as-a-Service (IaaS) providers is supported if all supportability requirements are met. In the case of providers who are provisioning virtual machines, these requirements include ensuring that the hypervisor being used for Exchange virtual machines is fully supported, and that the infrastructure to be utilized by Exchange meets the performance requirements that were determined during the sizing process. Deployment on Microsoft Azure virtual machines is supported if all storage volumes used for Exchange databases and database transaction logs (including transport databases) are configured for Azure Premium Storage.



  - The Exchange guest virtual machine has the following conditions:
    
      - It's running Exchange 2013.
    
      - It's deployed on Windows Server 2008 R2 SP1 (or later versions), Windows Server 2012, or on Windows Server 2012 R2.

For deployments of Exchange 2013:

  - All Exchange 2013 server roles are supported in a virtual machine.

  - Exchange server virtual machines (including Exchange Mailbox virtual machines that are part of a database availability group, or DAG), may be combined with host-based failover clustering and migration technology, as long as the virtual machines are configured such that they won't save and restore state on disk when moved or taken offline. All failover activity occurring at the hypervisor level must result in a cold boot when the virtual machine is activated on the target node. All planned migration must either result in shutdown and cold boot, or an online migration that makes use of a technology like Hyper-V Live Migration. Hypervisor migration of virtual machines is supported by the hypervisor vendor; therefore, you must ensure that your hypervisor vendor has tested and supports migration of Exchange virtual machines. Microsoft supports Hyper-V Live Migration of these virtual machines.

  - Only management software (for example, antivirus software, backup software, or virtual machine management software) can be deployed on the physical host machine. No other server-based applications (for example, Exchange, SQL Server, Active Directory, or SAP) should be installed on the host machine. The host machine should be dedicated to running guest virtual machines.

  - Some hypervisors include features for taking snapshots of virtual machines. Virtual machine snapshots capture the state of a virtual machine while it's running. This feature enables you to take multiple snapshots of a virtual machine and then revert the virtual machine to any of the previous states by applying a snapshot to the virtual machine. However, virtual machine snapshots aren't application aware, and using them can have unintended and unexpected consequences for a server application that maintains state data, such as Exchange. As a result, making virtual machine snapshots of an Exchange guest virtual machine isn't supported.

  - Many hardware virtualization products allow you to specify the number of virtual processors that should be allocated to each guest virtual machine. The virtual processors located in the guest virtual machine share a fixed number of physical processor cores in the physical system. Exchange supports a virtual processor-to-physical processor core ratio no greater than 2:1, although we recommend a ratio of 1:1. For example, a dual processor system using quad core processors contains a total of 8 physical processor cores in the host system. On a system with this configuration, don't allocate more than a total of 16 virtual processors to all guest virtual machines combined.

  - When calculating the total number of virtual processors required by the host machine, you must also account for both I/O and operating system requirements. In most cases, the equivalent number of virtual processors required in the host operating system for a system hosting Exchange virtual machines is 2. This value should be used as a baseline for the host operating system virtual processor when calculating the overall ratio of physical cores to virtual processors. If performance monitoring of the host operating system indicates you're consuming more processor utilization than the equivalent of 2 processors, you should reduce the count of virtual processors assigned to guest virtual machines accordingly and verify that the overall virtual processor-to-physical core ratio is no greater than 2:1.

  - The operating system for an Exchange guest machine must use a disk that has a size equal to at least 15 gigabytes (GB) plus the size of the virtual memory that's allocated to the guest machine. This requirement is necessary to account for the operating system and paging file disk requirements. For example, if the guest machine is allocated 16 GB of memory, the minimum disk space needed for the guest operating system disk is 31 GB.
    
    In addition, it's possible that guest virtual machines may be prevented from directly communicating with Fibre Channel or SCSI host bus adapters (HBAs) installed in the host machine. In this event, you must configure the adapters in the host machine's operating system and present the logical unit numbers (LUNs) to guest virtual machines as either a virtual disk or a pass-through disk.

  - The only supported way to send emails to external domains from Azure compute resources is via an SMTP relay (otherwise known as an SMTP smart host). The Azure compute resource sends the email to the SMTP relay and then the SMTP relay provider delivers the email to the external domain. Microsoft Exchange Online Protection is one provider of an SMTP relay, but there are a number of third party providers as well. For more information, see the Microsoft Azure Support Team Blog post [Sending E-mail from Azure Compute Resource to External Domains](https://go.microsoft.com/fwlink/p/?linkid=799723).

Return to top

## Host machine storage requirements

The minimum disk space requirements for each host machine are as follows:

  - Host machines in some hardware virtualization applications may require storage space for an operating system and its components. For example, when running Windows Server 2008 R2 with Hyper-V, you will need a minimum of 10 GB to meet the requirements for Windows Server 2008. For more details, see [Windows Server 2008 R2 System Requirements](https://go.microsoft.com/fwlink/p/?linkid=125378). Additional storage space is also required to support the operating system's paging file, management software, and crash recovery (dump) files.

  - Some hypervisors maintain files on the host machine that are unique to each guest virtual machine. For example, in a Hyper-V environment, a temporary memory storage file (BIN file) is created and maintained for each guest machine. The size of each BIN file is equal to the amount of memory allocated to the guest machine. In addition, other files may also be created and maintained on the host machine for each guest machine.

  - If your host machine is running Windows Server 2012 Hyper-V or Hyper-V 2012, and you are configuring a host-based failover cluster that will host Exchange Mailbox servers in a database availability group, then we recommend following the guidance documented in Microsoft Knowledge Base article, [2872325, Guest Cluster nodes in Hyper-V may not be able to create or join](https://support.microsoft.com/kb/2872325).

Return to top

## Exchange storage requirements

Requirements for storage connected to a virtualized Exchange server are as follows:

  - Each Exchange guest machine must be allocated sufficient storage space on the host machine for the fixed disk that contains the guest's operating system, any temporary memory storage files in use, and related virtual machine files that are hosted on the host machine. In addition, for each Exchange guest machine, you must also allocate sufficient storage for the message queues and sufficient storage for the databases and log files on Mailbox servers.

  - The storage used by the Exchange guest machine for storage of Exchange data (for example, mailbox databases and transport queues) can be virtual storage of a fixed size (for example, fixed virtual hard disks (VHD or VHDX) in a Hyper-V environment), dynamic virtual storage when using VHDX files with Hyper-V, SCSI pass-through storage, or Internet SCSI (iSCSI) storage. Pass-through storage is storage that's configured at the host level and dedicated to one guest machine. All storage used by an Exchange guest machine for storage of Exchange data must be block-level storage because Exchange 2013 doesn't support the use of network attached storage (NAS) volumes, other than in the SMB 3.0 scenario outlined later in this topic. Also, NAS storage that's presented to the guest as block-level storage via the hypervisor isn't supported.

  - Fixed or dynamic virtual disks may be stored on SMB 3.0 files that are backed by block-level storage if the guest machine is running on Windows Server 2012 Hyper-V (or a later version of Hyper-V). The only supported usage of SMB 3.0 file shares is for storage of fixed or dynamic virtual disks. Such file shares can't be used for direct storage of Exchange data. When using SMB 3.0 file shares to store fixed or dynamic virtual disks, the storage backing the file share should be configured for high availability to ensure the best possible availability of the Exchange service.

  - Storage used by Exchange should be hosted in disk spindles that are separate from the storage that's hosting the guest virtual machine's operating system.

  - Configuring iSCSI storage to use an iSCSI initiator inside an Exchange guest virtual machine is supported. However, there is reduced performance in this configuration if the network stack inside a virtual machine isn't full-featured (for example, not all virtual network stacks support jumbo frames).

Return to top

## Exchange memory requirements and recommendations

Some hypervisors have the ability to oversubscribe or dynamically adjust the amount of memory available to a specific guest machine based on the perceived usage of memory in the guest machine as compared to the needs of other guest machines managed by the same hypervisor. This technology makes sense for workloads in which memory is needed for brief periods of time and then can be surrendered for other uses. However, it doesn't make sense for workloads that are designed to use memory on an ongoing basis. Exchange, like many server applications with optimizations for performance that involve caching of data in memory, is susceptible to poor system performance and an unacceptable client experience if it doesn't have full control over the memory allocated to the physical or virtual machine on which it's running. As a result, using dynamic memory features for Exchange isn't supported.

Return to top

## Host-based failover clustering and migration for Exchange

The following are answers to some frequently asked questions about host-based failover clustering and migration technology with Exchange 2013 DAGs:

  - **Does Microsoft support third-party migration technology?**
    
    Microsoft can't make support statements for the integration of third party hypervisor products using these technologies with Exchange, because these technologies aren't part of the Server Virtualization Validation Program (SVVP). The SVVP covers the other aspects of Microsoft support for third-party hypervisors. You need to ensure that your hypervisor vendor supports the combination of their migration and clustering technology with Exchange. If your hypervisor vendor supports their migration technology with Exchange, Microsoft supports Exchange with their migration technology.

  - **How does Microsoft define host-based failover clustering?**
    
    Host-based failover clustering refers to any technology that provides the automatic ability to react to host-level failures and start affected virtual machines on alternate servers. Use of this technology is supported given that, in a failure scenario, the virtual machine is coming up from a cold boot on the alternate host. This technology helps to make sure that the virtual machine never comes up from a saved state that's persisted on disk because it will be stale relative to the rest of the DAG members.

  - **What does Microsoft mean by migration support?**
    
    Migration technology refers to any technology that allows a planned move of a virtual machine from one host machine to another host machine. This move could also be an automated move that occurs as part of resource load balancing, but it isn't related to a failure in the system. Migrations are supported as long as the virtual machines never come up from a saved state that's persisted on disk. This means that technology that moves a virtual machine by transporting the state and virtual machine memory over the network with no perceived downtime is supported for use with Exchange. A third-party hypervisor vendor must provide support for the migration technology, while Microsoft provides support for Exchange when used in this configuration.

Return to top
