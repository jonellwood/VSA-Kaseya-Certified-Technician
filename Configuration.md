
# Configuration Steps

- Once you are ready for your first agent deployment, you can either use the "Default Install" package or you can create a custom one.

## Agent Manual Deployment

- Kaseya offers two methods for installing/deploying the Kaseya Agent, manually via the Agent module or automatically via Discovery

### What is Manual Installation?

- Manual Installation refers to a non-automated installation of the Kaseya Agent on a managed system. This process entails logging into the managed device and executing the Kaseya Agent installation software (KcsSetup.exe) on it.

	### Methods for manually installing the Kaseya Agent on endpoints:
	1. You can provide the URL to the installer package directly to an end-user and instruct them to download/execute it on their end.
	2. You can provide the Kaseya Agent installer file called "KcsSetup.exe" or share it with the end-user.

! Agent packages will not be listed on a public Download page, but custom packages can be downloaded without authentication using a known link provided by the VSA Admin user.

! Clicking the "Download Package" link will immediately download the agent package while selecting the agent package name will trigger a pop-up window with more options.

! The installer package link must be externally accessible. When a VSA is behind a VPN, or when a firewall links directly to the Kaseya VSA, it may not function correctly.

### Installation

- Once the Kaseya Agent installer file is downloaded using one of the methods we discussed in the previous lesson, it will need to be executed with Administrative level credentials to properly place all program files. 

 - once isntalled you will be able to find your new agent in the VSA under **Agent>Manage Agents**

 - Once the Kaseya Agent is installed on a managed endpoint, it will display a Kaseya Agent icon in the system tray area. Right click the icon to display the agent menu

- You will also find the "kworking" folder for your Kaseya Agent.

! You can customize the Kaseya Agent icon to display a custom image instead of the default one

- The kworking directory will get recreated in the event this folder gets accidentally deleted. 

- Kaseya Agent and Kaseya Agent Endpoint services will be running

### A couple of things

- After the Kaseya Agent package is installed, the status of the Kaseya Agent software can be reviewed from the VSA. Logging into the VSA and reviewing the Manage Agents page will show the status of your agents.

- The circle next to Machine ID is the agent check-in status icon. There are various agent statuses depending on the machine state.

! The icon shown in the Kaseya VSA Framework depends on the Kaseya Agent status. The icon states will change based on the status of the computer. Status indicate whether it is being actively used, if a user is logged in, or if the agent is simply offline.
	- Each icon indicates a different state for the managed endpoint: 
		- green with clock = online waiting for first audit to complete 
		- green = Agent online
		- blue = Agent online and user currently logged in and active
		- yellow = Agent online - not active but currently logged in
		- gray = The agent is currently offline
		- orange = the agent has never checked in
		- green/red = Agent is online but remote control has been disabled
		- red = This account has been suspended


## Agent Auto Discovery and Remote Deploy

- That's where Discovery comes in handy, as it offers the ability to install agents remotely and automatically over a network-based or domain-based environment

**MANUAL DEPLOYMENT** 
- Allows for the install to be more hands-on and customizable on an individual endpoint basis.
- Allows you to decide if an agent is needed on a device on an individual basis.
- Allows you to account for different local administrative credentials that are needed for different endpoint installs.
- Allows you to assign different agent packages for different endpoints on the same environment (e.g. agent package for server-based or workstation-based endpoints.)

**AUTOMATED DEPLOYMENT**
- More hands-off approach and allows for true automation of agent deployments.
- Can deploy an agent to an endpoint as soon as a network or domain scan is performed.
- When this option is paired with Policy Management, devices can be found automatically and Kaseya-based settings can be implemented with very little to no user interaction.

## Types of Discovery Deployments

Discovery allows you to discover computers and devices on individual networks by Network (called LAN Watch) or by entire domains (called Domain Watch). Read more about each of these below:

**LAN WATCH**
- Discovers computers and devices on individual networks.
- Deploys agents to discovered agentless machines.
- Finds devices that are not eligible for an agent for inventory purposes (e.g. printers, switches, routers, etc.)
- Identifies SNMP devices and vPro machines.
- Enables a device to be "promoted" to a managed asset.

**DOMAIN WATCH**
- Automatically discovers AD domains that can be synced with the Kaseya Server.
- Automatically keeps the VSA synchronized with all domain changes.
- Auto-deploys agents to domain computers. Agents are automatically placed in the appropriate machine group relative to the domain hierarchy and organizational unit structure.
- Deploys agents across subnets and vLANs that are part of a domain.

Kaseya **Network Discovery** can discover computers and devices on individual networks. Once a computer is discovered, an agent can be remotely deployed to an agentless machine. This type of discovery provides the ability to create networks with specific agents, run a scan from an individual agent, or import networks from an XML file. 

Computers and devices that are found, regardless if there is an agent installed or not, can appear as assets. When an agent cannot be installed on a discovered device, the device can be promoted to a managed asset. For example, a router or printer may still require monitoring, even if an agent cannot be installed on the machine.

LAN WATCH = Deploy Agent => Select Network => Edit LAN Watch Settings => Set Agent Deploy Polices => Run LAN Watch. Deploy Agents. View Results.

! You must have an agent installed on at least one machine on the network being scanned in order for devices to be found.

## Discovery by Network

The **Discovery > Networks > By Network** function allows you to discover computers and devices on LANs. To scan a network, select the row of a detected LAN, click on New or Edit to set the scan properties and lastly, schedule a scan once or on a recurring basis using the Schedule Scan button. You can also run a scan immediately using the Scan Now button.

Not only are the above functions available to you on the By Network page, but five new tabs will also appear upon creating a network. 

Network Probe - This tab displays the agent machine performing the discovery scan on a network. This tab will also contain the probe agent information.

Scan Schedules - This tab allows you to keep recurring scan schedules for a selected network. It also allows for the addition, modification, or deletion of scan schedules.

Agent Deployment Policy - This tab allows you to set policies for the deployment of agents on computers discovered on a selected network.

Alerting Profiles - This tab allows you to set discovery alert policies for a selected network and device type including computer, mobile, network, and firewall.

Alerts can be flagged if a new device has been found or if the IP address, associated with an existing MAC address, has been changed. Alerts can also be configured to either create an alarm or ticket, send an email, or run an Agent procedure on an agent.

Asset Promotion – This tab allows you to configure the automatic promotion of devices to assets when the devices are discovered.

## Discovery by Agent

The **Discovery > Networks > By Agent** page allows you to discover devices on the same LAN as a selected probe machine - devices can be workstations and servers without agents.

! This is the fastest way to scan a new network By Agent.

## LAN Scan Process

**QUICK SCAN**
- Utilizes NMAP to find all the known IP addresses within a given LAN Scan range.
- Results are written to <agent working directory>\LanWatch\temp\nmapps-out-<GUID>.xml

**DNS SCAN**
- Utilizes kPrtPng.exe to find device names and MAC addresses.
- Not all devices will allow for their device name to be shown. If the device name is not found, the device will be named unknown-<MAC Address>
- Results are written to <agent working directory>\LanWatch\temp\dns-unk-<GUID>.xml

**DEEP SCAN**
- Utilizes NMAP to get detailed results back ranging from ports open, OS matching, and networking metrics.
- Results are written to <agent working directory>\LanWatch\temp\nmapos-<GUID>.xml

The Discovered Devices page shows computers and devices discovered using Discovery by Network and Discovery by Agent. Use this page to install agents on discovered computers. 

## Topology Map ##

The Topology Map is an interactive map that displays information about networks, devices within a network, types of devices, device status, and how they are connected. All connections between devices are determined by data collected using the SNMP protocol.

As a VSA user, you can quickly deploy simple SNMP monitoring to standard network infrastructure and printers by right-clicking the **Enable Monitoring** button on an eligible SNMP node on the **Discovery > Networks > Topology Map** tab. Eligible nodes are SNMP nodes that are printers, routers, switches that have been promoted to assets and do not currently have standard monitoring enabled. If a device is *not* an asset, when the **Enable Monitoring** option is selected, it will be automatically promoted to an asset.

! If you don't have any networks set up under Discovery > Networks > By Network, you will not be able to interact with the Topology Map page. If you do have networks but these were set up before, please check their settings and re-run a scan to enable the Topology Map.

### Topology Map Views

The Topology Map has two variants of view: cluster and tree. You can switch from one to the other view by clicking on Cluster View/Tree View button in the bottom right corner.

- Also found in the bottom right corner is the time and date of the last network scan.
- Devices displayed on the map are equivalent to those that are displayed in the Discovery > Networks > Discovered Devices page.
- There may be two hubs displayed on the Topology Map. One hub contains the current network devices and the second, historical data. **Once discovered, a device will always be displayed even if it is not found in subsequent scans.**

### Device Status

Statuses of the devices are marked as colored circles around units:

- Solid green line = Online

- Solid gray line = Offline

- Dotted gray line = Unknown

**You can click on the different devices you see regardless of their status or OS. This will bring up the VSA's Quickview window.** 

The Quickview window shows information about the device and indicates that is not an asset nor an agent. Click on Scan Results or View Credentials.


## Domain Watch

Kaseya Discovery Domain Watch allows the ability to discover Active Directory (AD) domains and uses a probe agent on a domain controller endpoint to sync. Once synced, the probe harvests domain data back to the Kaseya Server. Domain Watch can be configured for Agent Deployment to domain machines using a Group Policy Object (GPO) to download the agent install package.

Under Domain Watch, a list of domains is presented based on endpoints belonging to a domain with an agent installed.

Domain Watch summary:

Deploy Agent => Select Domain => Deploy & Activate a Domain Probe => Set Agent Deployment Policies => Set Computer Policy => Set Content Policy => Apply Policies => Set Alerts => Schedule Periodoic Resync

! To work with an Active Directory domain, first deploy an agent to the Domain Controller. The system will automatically detect the name of the domain for each agent. The agent can then be selected and used as the AD probe machine.

The Domain Watch page allows you to configure the integration of Discovery with Active Directory domains. This configuration features include:

- Installing Discovery probes that monitor a domain.
- Scheduling the synchronization of data between Discovery and the domain.
- Applying Discovery policies for the deployment of agents.
- Setting Discovery alerts.
- Displaying the status of the Discovery configuration.

The **Probe Deployment** tab allows you to configure the probe agent for a selected domain. All domain computers with agnet installed on them display in the lower panel.

Discovery communicates wtih an A/D domain using a probe agent. When the probe is first installed a Preview Scan is performed. The Preview Scan updates Discovery with the summary of domain data for all Orginizational units and objects

The **Agent Deployment** tab allows you to set agent deployment policies for a selected domain. 

Here you can click edit to modify if agents get installed automatically after Domain policies are set,, if an agent can be isntalled on a domain controller, and what agent pkg will be used. 

The **Schedule and Status** tab allows you to schedule Full Sync for a selected domain. aka Harvest Scan provides Discovery with a complete update of domain data, including:

- Summary domain data for all OU's and Objects, wether included or excluded
- Detailed domain data for all included *folders* and included *items*

! Discovery communicates with an Active Directory domain using a probe agent. When the probe is first installed, a Preview scan is performed. The Preview scan updates Discovery with the summary of domain data for all organizational units and objects.

## Agent Endpoint Settings

The Kaseya Agent's Working Directory (kworking) is the folder on each managed machine used to store many Kaseya-related files. All managed machines have a defined working directory based on the Operating System of the managed machine. 

The Kaseya Server, also known as "KServer", will use the Working Directory folder on managed machines to transfer and store files related to Kaseya processes, data collection, monitoring, protection, and several other tasks.

### Best Practices ###

**Windows**

- In Windows, the default working directory is found in C:\kworking.
- You can customize the working directory to reflect your corporate brand or company name.
- Make sure to approve the working directory in security software, such as anti-virus, to ensure the agent can write and access the necessary files.
- The Network Services account must have access to the defined working directory.
- Do not delete any Kaseya-created files or folders from the Working Directory as the agent uses these files for various tasks.

! Do not use Microsoft OS controlled folders such as Temp, System, Program Files, or Windows directories as this can cause write, access, and other permissions issues for the Kaseya Agent.

**Mac**

- In Macs, the default working directory is found in /Library/Kaseya/kworking.
- You can customize the working directory to reflect your corporate brand or company name.
- Make sure to approve the working directory in security software, such as anti-virus, to ensure the agent can write and access the necessary files.
- Do not use directory paths controlled by Mac OS.

! Avoid using spaces in the Working Directory path. If spaces are necessary, each space must be preceded with a backslash.

**Linux**

- In Linux, the default working directory is found in /tmp/kworking.
- You can customize the working directory to reflect your corporate brand or company name.
- Do not use directory paths controlled by the Linux OS.

! It is also necessary that the Working Directory folder is not hidden. If hidden, Kaseya may not be able to complete some automated tasks, which could lead to undesirable results when running tasks, failures of agent procedures, and the inability to complete installations and properly monitor the managed machine.


### Setting the Working Directory ###

The Working Directory is required for the collection and distribution of files between the agent and the Kaseya Server. The Kaseya Agent will automatically create the kworking folder based on the configuration defined in the Agent module. 

Administrators can use the default directory or can define a customized folder. Many companies choose to use a folder which reflects their corporate brand.  

1. Navigate to **Agent > Manage Agents** ... by default you may not see the *Working Directory* column
2. Click on the down arrow to add a column

### Configuring the Agent Menu ###

The Agent Menu page in the Agent module provides you the ability to select which options appear in the Agent Menu on the managed endpoint. Some of the options, such as About and Contact Helpdesk, can be customized to reflect a corporate brand. 

Once you've decided what options you will make visible to the end-user, simply uncheck the ones you want to hide from view, select the agent to apply these settings to, and click the Update button.

You will then see the text for your agent in the VSA turn red. This means that the changes are pending until the next time the agent checks in. At the next check-in, it takes only a few seconds for the endpoint to apply your new settings which will be then reflected in the UI.

## Setting Credentials ##

The Set Credential function in the Agent module allows you to define the username and password to be leveraged for some Kaseya-invoked processes. 

The defined credentials are used to impersonate the user login for access or execution of resources and tasks that require administrator privileges. This includes access to a file share or execution of an installer.


### Best Practices ###

- The Set Credential account must exist as a Local User Account or must be an existing Domain User Account. This function does not create the account on the machine or domain.  
- When using a Local User account, the Set Credential should be a member of the Local Administrators Group to ensure the Kaseya Agent can successfully complete assigned tasks which may require administrator rights. 
- When using a Domain account, the Set Credential should be a member of the Domain Administrators Group. Additionally, Group Policy should not restrict the ability to execute files or access necessary file shares or servers for the defined Set Credential account.
- Run a credential test after any changes to the credentials and as a preliminary step for any troubleshooting. Many processes will fail if the Set Credential is inaccurate or the account is locked.

The Set Credential function provides you the ability to test the defined username and password. This test will perform tasks to verify whether the account: exists, is active (not locked out), has access to write to the kworking directory and if it has access to execute from the kworking directory.

As part of this process, the credentials will be tested using the password provided. If the password is incorrect or if any of the above items return as unsuccessful, the credential test will fail.

Setting the credentials - 

Navigate to **Agent > Manage Agents** and select the agent youd like to set credentials on and click the credentials button. Then select the first option, **Set Credentials**

! You can set the same credentials on multiple agents as long as the credentials exist on each of the managed endpoints.

## Updating the Agent ##

Periodically, it is necessary to update the agent software that resides on a managed machine. This update does not automatically occur when the Kaseya Server is upgraded - you must schedule the agent update on managed machines.

Usually, with every VSA patch release, there is a new agent version that comes with it. We strongly recommend that you update your agents when a new agent version is released.

### Best Practices ###

- The Kaseya Agent should always be at the version the Patch Release Notes link specifies.
- Schedule these agent updates when new software is released. Agent updates are released to add enhancements and address defects or vulnerabilities.
- Use the Post Procedure function to reboot a computer or run a specific agent procedure after the update completes. By assigning the Post Procedure, you can automate post-update tasks.

Navigate to **Agent > Manage Agents** by default you should see the agent version column. Compare the version to the one the **Manage Agents** page lists and determin if it needs updating. Click on the **Manage** button and select **Update Agents**

! If you are an On-Premise Customer, you will have access to the Automatic Update page in the Agent module. This page allows you to automatically update your agents to the latest version. Note that scheduling is staggered to avoid bandwidth issues. 

## Agent VSA Settings ##

The Kaseya VSA includes several logs used to record various activities. Many of these logs are related to the interaction between the Kaseya Server and the managed machines.

You can define the length of time these log entries are retained in **Agent > Log History**. The retention period is important as the ability to review and run reports against these entries require they remain available in the database.

! Kaseya agent logs default to a 30 or 31 day retention period. You can adjust these settings depending on the needs of your company.

### Log Types ###
"Agent > Agents > Agent Logs"

**Configuration Changes**

This log displays agent-specific adjustments. This includes items such as the assignment of schedules, changes to a file source, assignment of a LAN Cache, and other endpoint-specific changes.

Note: The VSA account responsible for the change is recorded and available for review. Use this log to determine which VSA user adjusted the settings for a specific agent.

**Network Stats**

This log displays send/receive data for network applications.

**Procedure History Log**

This log displays information related to the Agent Procedures, or scripts, that run on an endpoint as well as the success or failure of the tasks. Depending on the Agent Procedure or script, each task may write several entries to this log.

Note: The VSA account responsible for the running of the procedure is associated with each entry in the Procedure History Log. Use this log to identify the individual responsible for running the task as well as troubleshooting which step within a script a specific procedure may be failing.

**Classic Remote Control Log**

This log maintains the activity related to change in the Remote Control configuration such as defining notifications, installation of KVNC, and initiating KVNC or RDP connections.

**Remote Control / Live Connect logs**

This log maintains the activity when KRC/KLC are used to connect to a remote machine. Logged activity includes start time, end time, remote host ended the session, admin ended the session, session was ended unexpectedly, length of session, session admin name and the full display name of the remote machine.

**Alarm Log**

This log lists all alarms triggered for the selected machine.
Alarms are part of the Monitor module and can be reviewed in the Monitor > Alarms page as well.  

**Monitor Action**

This log displays the alert conditions that have occurred, as well as the corresponding action taken (if any). Alert conditions are configured in the Monitor > Alerts page.

Note: A counter value of -998 in the monitor logs indicates the monitor set is returning no data. Check that the Performance Logs & Alerts service in Windows is running. This is a pre-requisite for monitoring performance counters.

**SYS Log**

This log displays data collected from standard text-based log files on the managed machine. Log monitoring extends that capability by extracting data from the output of any text-based log file.

Note: To avoid uploading all the data contained in these logs to the Kaseya Server database, log monitoring uses parser definitions and parser sets to parse each log file and select only the data you're interested in.

**Agent Uptime Log**

This log records the active and inactive time of the agent. If the number of days is set to zero, the agent uptime will not be recorded and cannot be reported on.

Note: Kaseya recommends the Agent Uptime Log be configured to collect at least one day of data, though you may choose to retain these logs for longer periods. This log is useful in troubleshooting agent check-in issues and for reporting overall uptime.

### Retention Periods ###

**Extended Retention**

You may choose to increase log retention to allow for longer reporting. In some cases, you may elect to increase a retention period to capture data from a sporadic issue that may occur at intervals longer than the standard retention.  

! Example: An issue that seems to appear "every month" or so might require you to track logs for several months in a row to capture and identify behavioral patterns. In this case, it might be necessary to increase a log to a 60 or 90 day period.  It is important to consider, however, that the data will be stored in the database. Unnecessary and excessive log retention may impact Kaseya server performance.

**Limited Retention**

A shorter retention period may be sufficient for some machines or for some log types. This potentially reduces the amount of data stored in the database. The shorter retention may require reports to be run on a schedule in line with the defined retention period.

! Example: A client or manager expects to receive a report of all Remote Control activity against specific managed machines for each month but the retention period for the Remote Control log is set for 15 days. It would be necessary to schedule a Remote Control Log report to run approximately twice a month to gather a full month worth of data. Reports will be covered in an upcoming lesson.

### Event Logs ###

Microsoft Windows Event Logs can be monitored and reviewed from within the VSA. You may elect to enable the collection to allow for reporting.

Events tab in the Agent > Agent Logs page.

!The collection of these log entries to the database is not required for review.  

### Agent Account in the VSA ###

You will find several buttons in **"Agent > Manage Agents"** that will allow you to interact with the agent. For now, we will cover the ones under "Manage".

**Update Agents**

Updates selected agents with the latest version of the agent software. 

Note: Updating the agent software makes no changes to the agent settings you have defined for each agent. 

**Cancel Update**

Cancels a pending update on selected managed machines. 

**Delete Agents**

Deletes three different combinations of machine ID accounts and agents:

- **Uninstall agent first at next check-in** - Uninstall the agent from the machine and remove the machine ID account from the Kaseya Server. The account is not deleted until the next time the agent successfully checks in.- **
- **Delete account now without uninstalling the agent** - Leave the agent installed and remove the machine ID account from the Kaseya Server.
= **Uninstall the agent and keep the account** - Uninstall the agent from the machine without removing the machine ID account from the Kaseya Server.

! Note: If you'd like to reclaim the agent license right away, use the second option.

**Cancel Delete**

Cancels a pending delete on selected managed machines.

**Rename**

Renames an existing machine ID account. You can also assign the machine to a different machine group. Renaming an agent only changes how the name is displayed in the VSA. 

Use merge to combine log data from two different accounts into the same machine. This could be necessary if an agent was uninstalled and then re-installed with a different account name. Merge combines the accounts as follows:

- Log data from both accounts are combined.
- Baseline Audit data from the old offline account replaces any baseline data in the selected account.
- Alert settings from the selected account are kept.
- Pending agent procedures from the selected account are kept. Pending agent procedures from the old offline account are discarded.
- The old account is deleted after the merge.

**Change Group**

Assigns multiple agents to a different machine group. Machines currently offline are assigned the next time they check in. Changing the machine group may trigger automated actions. For example, **Policy Management** may apply different policies, based on the the assigned machine group.

**Working Directory**

Sets the path to a directory on the managed machine used by the agent to store working files. Depending on the task at hand, the agent uses several additional files. 

The server transfers these files to a working directory used by the agent on the managed machine. For selected machine IDs you can change the default working directory from C:\kworking to any other location. 

! Note: You can approve this directory in security programs, such as virus checkers, to allow operations such as remote control from being blocked.

**Suspend/Resume**

Suspends/resumes all agent operations such as agent procedures, monitoring, and patching without changing the agent's settings. While a machine ID account is suspended, the managed machine displays a gray agent icon in the system tray.

! Note: Suspending an agent does not release the associated agent license. You will need to use the Delete Agents function to reclaim agent licenses.

## Lan Cache ##

The LAN Cache page designates a machine to act as a file share for other endpoints on the same LAN. This process speeds up delivery to various machines, reducing network bandwidth issues. 

When a machine assigned to the LAN cache requests a download from the Kaseya Server for the first time, files are downloaded to the LAN cache machine, then copied to the requesting endpoint. From then on, the file does not need to be downloaded from the KServer - any other endpoint in the same LAN can obtain the same file from the LAN cache machine from that point forward. 

LAN Cache configures a file source as follows:

- Automatically creates a local administrator, or domain administrator account, or allows the ability to manually specify the credential for an existing domain administrator. 
- Once the password is generated, it is compared against the admin name to ensure that no two-character combinations in the password match any two-character combinations in the admin name. This logic ensures that the generated passwords will meet any Windows password complexity logic.
- The credentials for the account are associated with this LAN cache within Kaseya and are used when necessary instead of any assigned agent credential. LAN Cache does not require nor support using the credential specified on the Agent > Manage Agents > Credentials function.
- Creation of the specified share directory on the specified fixed disk drive configured as a Windows administrative share. The directory and share are created without leaving the LAN Cache page.
- Creation of a special Kaseya directory, always called VSAFileShare under the Kaseya directory, on the specified fixed disk drive configured as a Windows administrative share.
- LAN cache is limited based on Microsoft Windows limitations regarding total amount of concurrent connections to a File Share.

! Created accounts are given a unique name (FSAdminxxxxxxxxx where x is a digit) with an automatically generated password. The generated password contains 15 randomly selected characters and contains at least one of the following character types: uppercase letters, lowercase letters, numbers (0 - 9) and non-alphanumeric characters.

### Creating a LAN Cache ###

To assign a LAN cache, select the desired agent and click on "Add LAN Cache". Keep in mind that the machine functioning as a LAN cache will only service machines on the same network.

1. Enter a descriptive and distinct name for the LAN cache as it will be displayed when assigning the LAN cache to endpoints that will receive files. 
2. Enter the name of the directory only without specifying the name of the machine or the drive letter. The directory does not have to already exist. The LAN cache will create the directory and the required share settings. Consider making the folder name descriptive so that endusers can quickly identify the folder as non-malicious.
3. Specify the UNC name resolution format used to access the share. E.g. \\computername\sharename$ or \\10.10.10.118\sharename$.
4. If auto-generated administrator credentials are selected, an administrator credential is created for you when the LAN cache is created. A local administrator credential is created unless the machine is a domain controller. If the machine is a domain controller, use the latter option to utilize an existing domain administrator's credentials.
5. Select the drive to create the LAN cache file share on.

### Assigning a LAN Cache ###

Navigate to the **Agent > Configure Agents > Assign LAN Cache** page to assign and remove machines from a selected LAN cache. After assigning to the corresponding machines, the agents will show as follows in the VSA.

Here you will also be able to test the assigned LAN cache functionality and clear any pending tests.

! After LAN cache assignment, you should test the assigned LAN cache functionality. You will see the test in "Pending" status until it passes or fails. Remember that you can clear any tests at any time by clicking the Clear Pending button.

## Agent Information ##

Every Kaseya Agent that is installed will report back data and informational records to the Kaseya VSA Server. This information is stored and associated with the individual agent. The data may then be used by the Kaseya Server to process certain requests or the data may be logged for tracking purposes

### What is Kasaya Agent Information? ###

Kaseya Agent Information is any log or agent/machine specific information associated with an individual computer or machine.

The entire capacity of this information is tied to the individual Kaseya Agent within the Kaseya VSA.

If the Kaseya Agent is deleted from the Kaseya VSA this information will be removed as well.

**What are some examples of Kasaya Agent Information?

Examples of Kaseya Agent Information include Agent Logs, Windows Event Logs, Procedure History Logs, and Machine Specific Information.

Also, custom information can be created and documented on an Agent specific basis. Information such as Special Instructions, Contact Information, and Notes.

**Is this information needed?"

These records can provide unique and important information about individual endpoints, which can be readily available to various VSA Users.

This information can be used to track agent-specific activity, monitor configuration changes, and review agent or event logs.

### Quickview ###

Quickview provides a limited window-based version of Kaseya Live Connect. To access Quickview, hover over any Agent icon located inside the Kaseya VSA.

! By default, moving the cursor outside of the Quickview window will make the Quickview window disappear. Don't worry though, you can pin it and even navigate to a different module without losing sight of it!

### Column Sets ###

The Manage Agents page provides an overall summary for every Kaseya Agent in the VSA and you can add or remove columns as needed. Alternatively, you can create Column Sets to allow for easier access to these columns and summaries without having to add or remove them every time you need them.

You can also quickly edit and delete Column Sets or manage them via the Manage button.

To create a new Column Set, simply drag and drop the available columns from the left to the right and click "Save".

! After you save the new Column Set, you will not see any change in the Manage Agents page. You'll need to select the newly created Column Set from the drop-down menu on the right side of the screen for the grid to update and show the columns you had previously selected.

You can also export the results from the page/grid, refresh it, or simply reset to the original columns.

### Views ###

Agent Views allow filtering and sorting options within the VSA to classify and view certain machines. This comes in handy whenever you'd like to look for a group of agents matching specific criteria.

Custom Views can be created using the New and Edit buttons. Pre-defined or pre-built Views are also available in the View drop-down list. Views can be cleared using the Reset button.

To create a new view, click the "New" or "Edit" buttons and then "Save As" to get started.

Following the example used above, you want to identify Windows systems that have been online in the last 4 hours.  To do this, you need to specify the OS Type and a Machine Status:

!Once you click Save you will see the background page refresh. This doesn't mean that the actual Manage Agents grid will show you updated results; you'd need to select the view manually from the drop-down menu after exiting out of the View Definitions pop-up window.

## Agent Profiles ##

Agent profiles have the capability to associate and store individual agent settings and information within the Kaseya VSA. Type of information that can be stored on an Agent profile include:

- Agent profiles can contain contact information, the language preference for the Agent Menu on the user's machine and notes about each Machine ID or Group ID account.
- Agent Profiles also allows the option for special icon badges to indicate critical or important machines.
- Special instructions can be noted for individual or unique machines.

### Agent Profile in the VSA ###

To add a badge and special instructions to an Agent, follow these steps below:

1. Edit Profile 
2. Check little box on left hand side by "Notes"
3. Select "change" upper right near Icon Badge 
4. Select the badge from the "Select Badge" pop up
5. Click update

! Once you've added badges and/or special instructions on your agent(s), you will see the notes next to the Machine ID and the badge overlapping with the Agent icon. Now, if you hover over the agent icon to open up Quickview, the first thing you will see is the instructions you've just added. This comes in handy when it comes to giving other VSA users a head's up about a particular agent or group of agents.

## Branding the Agent Icon ##

Branding the Agent Icon allows your end-users to feel a sense of familiarity while increasing their connection to your company's reputation. 

Your users will be more comfortable seeing their MSP or internal IT Department's logo reinforced on the Agent Icon rather than the Kaseya logo. 

**Agent Icon in different Operating Systems**

- Windows - Windows icons must be in .ico format and the color depth must not exceed 256 colors. A maximum size of 32x32 pixels is recommended.

- Apple - Mac icons must be in .tif format and the color depth must not exceed 32-bit color. A maximum size of 48x48 pixels is recommended.

- Linux - Linux icons must be in .png format and the color depth must not exceed 256 colors. A size of 24x24 pixels is recommended.

### Setting the Agent Icons ###

The **Site Customization** page, under the **System** Module, gives you the ability to upload custom Agent Icons to the Kaseya VSA.

### Assigning the Agent Icons ###

To assign custom Agent Icons simply click the Edit button and decide which OS to modify: Windows, Mac, or Linux. 

You can click on the camera icon to search for the files you want to replace the current agent icon(s) with.

### Updating your Agents ###

Once the icon(s) is uploaded to the Kaseya VSA, downloaded agent packages going forward will have the updated agent icons for new agent deployments.

However, an Agent Update is required to push the custom Agent Icons to the endpoints. The customized Agent Icons are automatically deployed when updating agents via **Agent > Manage Agents > Manage > Update Agents**.

! It’s required that you check the "Force update even if agent is at version..." checkbox to update agents that are already at the current version allowing the new icon(s) to be applied. If the changes don't take effect.

## Branding the VSA ##

The Kaseya VSA can be branded to reflect specific branding, colors, and even philosophy. This action reinforces the corporate brand throughout the Kaseya VSA and the customers are using VSA. 

Branding will require photo editing, color selections, and company logos to be created and decided upon prior to implementation.

You are able to brand the following elements in the On-Prem version of the VSA:

- Kaseya VSA Logon Page

- Kaseya VSA Favorites Icon

- Kaseya VSA Site Header

- Kaseya VSA Site Header Image

- Kaseya Agent Icons

- Kaseya VSA Logon Page Image

- Kaseya Color Scheme

- Kaseya Deploy Header

You are able to brand the following elements in the SAAS (Software As A Service) version of the VSA:

- Kaseya VSA Site Header

- Kaseya VSA Site Header Image

- Kaseya Agent Icons

- Kaseya Color Scheme

- Kaseya Deploy Header

## Color Scheme ##

The Kaseya VSA color schemes are predefined and built for immediate use. 14 default color schemes are available within the Kaseya VSA. Find the one that suits your business the most!

It's only a matter of navigating to the Color Scheme page, selecting your desired color, and clicking the +Set Scheme button.

### Changing the Logon Page (On-Prem Only) ###

Custom imaging and wording can also be used to brand the Kaseya VSA. Customize the VSA Logo in "System > Customize > Site Customization".

! The path you choose for the Background Image must be relative to the Webpages directory, Webpages\Access directory, or a fully-formed URL.
! The logo will reflect across the header of the VSA on every page.

### Site Header ###

Note that the new VSA UI no longer supports Title next to the logo. Further, please keep in mind that the Favorites Icon is not supported in a Cloud-based VSA. 

### Creating a Unique Logon Page ###

Creating a unique logon page will require a custom .html page that replaces the "DefaultContent.htm" file. The replacement .html file will need to be placed in the :\Kaseya\WebPages\Access directory. Modifying "DefaultContent.htm" directly is not recommended as this file will be overwritten during patches and upgrades.

Once a new .html file is created, any images that will be referenced by the .html page need to be placed in the :\Kaseya\Webpages\images folder for correct re-direction.

Once the new logon page .html file is placed in the access directory and any associated images are placed in the images directory, the logon page can be changed in the Kaseya VSA.

! C:\Kaseya\WebPages\Access directory on the KServer.

**To create your unique logon page:**

1. Ensure all required files are located on the KServer, i.e. Downloads folder, Desktop, etc.

2. Place the .html file in :\Kaseya\WebPages\access.

3. Navigate back one directory and open folder "images"

4. Select and move the images that accompany the .html file from Step 2 to the :\Kaseya\WebPages\images directory.

5. Open a browser from inside the KServer and log into your VSA.

6. Navigate to the **System > Customize > Site Customization > Logon Page**.

7. Click **+Edit** and search for the image and right frame URL.

8. Click **Save**.

! All files must be placed on the Kaseya Server machine locally within the Kaseya install directory.

## Schedule and Execute Tasks ##

The Scheduler Utility allows you to define when specific tasks should run on managed machines and whether those tasks should recur at defined intervals. 

To access the Scheduler, you must first select at least *one* agent. The schedule defined will then be applied to the agents selected from the agent list.

### Scheduler Options ###

### "Distribution Window" Examples ###

Assuming there are five endpoints selected when the Scheduler is launched:

A schedule with a 'Run At' time of 10:00 am and no distribution window will schedule all five machines to begin the task at 10:00 am.

A schedule with a 'Run At' time of 10:00 am and a 10 minute distribution window will cause all machines to be assigned with a scheduled start time between 10:00 am and 10:10 am. Each machine will begin the execution of the task no later than 10:10 am.

A weekly schedule with a 'Run At' time of 10:00 am, a three-day distribution window, and with only Monday selected will cause all machines to be scheduled between 10:00 am on Monday and 11:59:59 on Wednesday. 

### "Skip if Offline" Examples###

_Example 1_: Weekly on Wednesdays at 10:00 am and "Skip if Offline" is selected. 

Behavior: Machine A1 is offline at 10:00 am. Machine A1 remains offline until 10:30 am. Since the 15 minute grace period has elapsed, the task has been skipped for this week and has been scheduled to run next Wednesday at 10:00 am.

_Example 2_: Weekly on Wednesdays at 10:00 am "Skip if Offline" is not selected. 

Behavior: Machine A1 is offline at 10:00 am. The task executes at 10:00 am and sits in the queue. When the agent checks, the task runs immediately. Any other queued tasks also run in the order in which they were placed in the queue. If the agent remains offline through the following Wednesday at 10:00 am, the next cycle will execute and sit in the queue. The same task may run multiple times on check-in if the agent remains offline throughout multiple schedule cycles.

### Scheduled vs. Immediate###

Tasks can be scheduled to run at a future date or time with or without recurrence. This is done through the Scheduler Utility we've been exploring. However, there are instances where you may want to run a task immediately. When troubleshooting, you can choose to run a task "now" without affecting the existing recurrence schedule.  

While the scheduler can be configured to run a scheduled task immediately, launching the scheduler and configuring a schedule requires some effort. This also overwrites the existing schedule. For one-time immediate execution of a task, consider using the Run Now function.

Run Now will appear next to the Schedule button for those tasks that support this particular function. When Run Now is selected, the task will be immediately queued, even if the agent is offline. The task will run as soon as the agent is checking in and once any other previously queued tasks are completed.

### Scheduler Variations###

The Scheduler utility is common in many modules throughout the VSA. However, the Scheduler may be slightly customized for some functions. For example, the Initial Update function of the **Patch Management** module only supports the recurrence type of "Once" because an Initial Update should not be scheduled to run on a recurring basis.  

The Run Audit function of the Audit module includes the ability to select which type of audit is to be scheduled so administrators and technicians can define the appropriate schedule for each audit type. These differences are based on the intended function of each function. However, the general functionality and use of the Scheduler utility will be the same throughout the VSA.

### Time Zone Considerations###

Time is a complex concept. In many cases, the endpoint, the Kaseya Server, and the VSA user scheduling a task may be in different time zones. Complicating the issue further, some global locations observe Daylight Saving Time (DST) during parts of the year while others do not. Even among areas where DST is observed, the dates for DST may vary from one location to another.  

For example, in areas of the United States that observe DST, the clock "springs forward" the second Sunday of March and "falls back" the first Sunday in November. In the European Union, Summer Time begins the last Sunday in March and ends the last Sunday in October. In New Zealand, DST begins the last Sunday in September and ends the first Sunday in April. For companies managing machines across time zones, determining when a task will run can be a very difficult undertaking.

Due to these variations, Kaseya provides you the ability to view schedules in the VSA based on the time zone of the Kaseya Server, the time reported by your web browser, or on a defined offset from Kaseya Server time. When scheduling a task, you can choose to define the schedule based on the agent time or based on the server time.

! Time Zone Offset from the System module and the Time Preference area of the Scheduler.

### Time Zone Examples###

KServer time: 6:00 PM UTC (aka GMT or Zulu Time)
Browser time: 1:00 PM Eastern (US) Standard Time (EST)
Agent time: 10:00 AM Pacific (US) Standard Time (PST)

To run a task after hours on the agent, choose "schedule in agent time" and, for example, 10:00 pm. The task will run at 10:00 pm based on the time zone defined in the agent's Operating System.

_Example:_ It's 10:00 am in your local time zone and you've been instructed to install a software package on all managed computers. The task must be completed in the next 2 hours. Your agents are spread around the globe. If you were to schedule the task to begin at 10:15 am with a 90 minute distribution window, but you chose to schedule based on the agent time, the machines within your time zone would be scheduled to run within the next 90 minutes. However, agents in other time zones would be scheduled to start the process within 90 minutes of their 10:00 am. That might be several hours from now. In this case, you'll want a task to run on a selection of computers at the exact same time, regardless of what time it might be in the agent's time zone. To accomplish this, run the task in server time (do not select Agent time).

## Import and Export##

The Kaseya VSA offers several tools to create individual content such as Agent Procedures, Monitor Sets, Reports, and Policies to name a few.

This content can be exported and/or imported from several locations within the VSA. The **Import Center** is the recommended tool included within the System Module that allows individualized content to be exported or imported within the VSA. It also allows bulk exporting and importing.

### How Does it Work?###

Import Center allows you to import or export multiple items or multiple item types of user-defined data structures into a single XML file. This XML file then contains all the content that was defined for import or export.

! The System > Server Management > Import Center page allows for imports and exports

! Modifications can be made directly to the XML which will have an *immediate* effect on content when uploaded through Import Center.

### Benefits###

Why is this beneficial?

- Import Center can be used as a backup option for important Agent Procedures, Monitors, or Policies in an XML that can be imported to restore content to its original state.
- The content found in the Kaseya Community can be exported and shared with others. Further, use the Import Center to import community content.
- Content and automation solutions can be migrated between VSAs or testing environments.

### Imports###

Importing an XML file is as simple as clicking on "New Import", selecting your file, and allowing the VSA to process it.

If desired, you can delete import entries, review any error messages, and set your settings via the "Edit Settings" button. This also controls the number of days to retain the import logs.

### Exports###

Exporting VSA files is as simple as clicking on "New Export", giving it a name, and selecting the Export Type of your choice. Then, either click "Continue" to keep adding objects to your export, or "Export" when finished.

! Example exports. The download link allows you to download the XML file for further use.

! You can export multiple items of varying types using a single XML. For example, you may want to import a set of Reports and Views that are both used together to form a single automation solution. 

---------------------------------------------------------------

Q: True or False: Once you are ready for your first agent deployment, you are required to create an agent package before you start deploying to machines.

A: False

Q: True or False: You can either deploy agents manually or automate this via the Discovery module.

A: True

Q: True or False: The Working Directory is not required for the collection and distribution of files between the agent and the Kaseya Server.

A: False

Q: What module/function allows you to define the length of time for which log entries are retained?

A: Agent > Log History

Q: True or False: When a machine assigned to the LAN cache requests a download from the Kaseya Server for the first time, files are downloaded to the LAN cache machine and then copied to the requesting endpoint. 

A: True

Q: True or False: Quickview provides a limited window-based version of Kaseya Live Connect.

A: True

Q: What Operating System(s) support the Agent Icon to be customized?

A: All of the above

Q: Select all that apply: What elements are you able to brand on the On-Premise version of the Kaseya VSA?

A: Kaseya VSA Logon Page, Kaseya VSA Favorites Icon, Kaseya VSA Site Header, Kaseya Color Scheme

Q: True or False: The Scheduler Utility allows you to define when specific tasks should run on managed machines and whether those tasks should recur at defined intervals. 

A: True

Q: True or False: The Kaseya VSA allows for the import and export of user-owned objects.

A: True
