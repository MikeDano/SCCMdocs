---
title: "Checklist for 1610 | System Center Configuration Manager"
description: "Learn about actions to take before updating to System Center Configuration Manager version 1610."
ms.custom: na
ms.date: 11/18/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: 7
author: Brendunsms.author: brendunsmanager: angrobe
---
# Checklist for installing update 1610 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
When you use the Current Branch of System Center Configuration Manager, you can install the in-console update for version 1610 to update your hierarchy from version 1606. If your hierarchy runs version 1511, 1602, or 1606, you can update to version 1610. 

To get the update for version 1610, you must use a service connection point site system role at the top-level site of your hierarchy. This can be in on-line or off-line mode. After your hierarchy downloads the update package from Microsoft, you will find it in the console under **Administration &gt; Overview &gt; Cloud Services &gt; Updates and Servicing**.

-   When the update is listed as **Available**, the update is ready to install. Before installing version 1610, review the following information [about installing update 1610](#about-installing-update-1610) and the [checklist](#checklist) for configurations to make before starting the update.

-   If the update displays as **Downloading** and does not change, review the **hman.log** and **dmpdownloader.log** for errors.

    -   Usually, you can also restart the SMS\_Executive service on the site server to restart the download of the updates redistribution files.

    -   Another common download issue is due to proxy server settings that prevent downloads from <http://silverlight.dlservice.microsoft.com> and <http://download.microsoft.com>.

For more information about installing updates, see [In-console updates and servicing](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

For information about the versions of the Current Branch, see [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines) in [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates).

## About installing update 1610

**Sites:**  
Update 1610 can only be installed at the top-level site of your hierarchy. This means you initiate the install from your central administration site if you have one, or from your stand-alone primary site. After the update installs at the top-tier site, child sites have the following update behavior:

-   Child primary sites install the update automatically after the central administration site completes installing the update. You can use service windows to control when a site installs updates. Prior to version 1606, service windows were called maintenance windows. For more information, see [Service Windows for site servers](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_ServiceWindow).

-   You must manually update secondary sites from within the Configuration Manager console after the primary parent site completes the update installation. Automatic update of secondary site servers is not supported.

**Site system roles:**  
When the site server installs the update, site system roles installed on the site server and those installed on remote computers automatically update. Therefore, before installing the update, make sure each site system server meets any new prerequisites for operation with the new update version.

**Configuration Manager consoles:**   
The first time you use a Configuration Manager consoles after the update completes, you will be prompted to update that console. To do so you must run Configuration Manager Setup on the computer that hosts the console, and select the option to update the console. We recommend that you do not delay installing the update to the console.



## Checklist

**Ensure all sites run a supported version of System Center Configuration Manager:** 
Before you start the installation of update 1610, each site in the hierarchy must run the same version of System Center Configuration Manager, either version 1511, 1602, or 1606.

**Review the status of your Software Assurance or equivalent subscription rights:**   
You must have an active Software Assurance (SA) agreement to install update 1610. When you install version 1610, you will have the option on the **Licensing** tab to confirm your **Software Assurance expiration date**. This is an optional value you can specify as a convenient reminder of your license expiration date that is visible when installing future updates. If you installed Configuration Manager from the version 1606 baseline media, you might have previously specified this value during Setup, or after the site installed on the **Licensing** tab of the **Hierarchy Settings**.

For more information see [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Review installed .NET versions on site system servers:** 
When a site installs update 1610, Configuration Manager automatically installs .NET Framework 4.5.2 on each computer that hosts one of the following site system roles when .NET Framework 4.5 or later is not already installed:

-   enrollment proxy point
-   enrollment point
-   management point
-   service connection point

This installation can put the site system server into a reboot pending state, and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might have random failures until the server is rebooted.

For more information see [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Review the site and hierarchy status and verify that there are no unresolved issues:** 
Before you update a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site update can fail due to existing operational problems.

For more information, see [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Review file and data replication between sites:**   
Ensure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth or successful update.\
For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update.

For more information, see [About the Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) in the [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) topic.

**Install all applicable critical updates for operating systems on computers that host the site, the site database server, and remote site system roles:** 
Before you install an update for Configuration Manager, install any critical updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the Configuration Manager update.

**Disable database replicas for management points at primary sites:**   
Configuration Manager cannot successfully update a primary site that has a database replica for management points enabled. Disable database replication before you:

-   Create a backup of the site database to test the database upgrade
-   Install an update for Configuration Manager

For more information, see [Database replicas for management points for System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Set SQL Server AlwaysOn availability groups to manual failover:**   
Before installing updates, like version 1610, ensure the availability group is set to manual failover. After the site updates, you can restore failover to be automatic. For more information see [SQL Server Always on for a site database](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure software update points that use NLBs:**   
Configuration Manager cannot update a site that uses a Network Load Balancing (NLB) cluster to host software update points.

If you use NLB clusters for software update points, use PowerShell to remove the NLB cluster.
For more information, see [Plan for software updates in System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Disable all site maintenance tasks at each site for the duration of the update installation on that site:**   
Before you install update, disable any site maintenance task that might run during the time the update process is active. This includes but is not limited to the following:

-   Backup Site Server
-   Delete Aged Client Operations
-   Delete Aged Discovery Data

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has installed.

For more information, see [Maintenance tasks for System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) and [Reference for maintenance tasks for System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Create a backup of the site database at the central administration site and primary sites:** 
Before you update a site, back up the site database to ensure that you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified
-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected
-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality
-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site
-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database

Configuration Manager does not support the backup of secondary sites nor the test upgrade of a secondary site database.

It is not supported to run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see the [Test the site database upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#bkmk_test) section in [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

**Plan for client piloting:**   
When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active client.

To take advantage of this option, before beginning installation of the update you must configure your site to support automatic upgrades for pre-production.

For more information, see [Upgrade clients in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) and [How to test client upgrades in a pre-production collection in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Plan to use service windows to control when site servers install updates:**   
You can use service windows to define a period that applies to a primary site server during which updates to that site can be installed.

This can help you control when sites in your hierarchy install the update. Prior to version 1606, service windows were called maintenance windows. For more information, see [Service Windows for site servers](/sccm/core/servers/manage/install-in-console-updates#bkmk_servicewindow).

**Run Setup Prerequisite Checker:**   
When the update is listed in the console as **Available,** you can independently run the Prerequisite Checker before installing the update. (When you install the update on the site, Prerequisite Checker runs again.)

To run a prerequisite check from the console, go to **Administration > Overview > Cloud Services > Updates and Servicing,** right click on **Configuration Manager 1610 update package**, and select **Run prerequisite check**.

For more information about starting and then monitor the prerequisite check, see **Step 3: Run the prerequisite checker before installing an update** in the [Install in-console updates for System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates) topic.

> [!IMPORTANT]  
> When the prerequisite checker runs as part of an update install or independently, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the 1610 update, if you must perform a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.

**Update sites:**   
You are now ready to start the update installation for your hierarchy. For information on installing the update, see [Install in-console updates.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

We recommend you plan to install the update outside of normal business hours for each site when the process of installing the update and its actions to reinstall site components and site system roles will have the least effect on your business operations. For more information, see [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates).
