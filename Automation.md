# Automation #

## Overview ##

**What is the ATSE code?**

The ATSE code is an acronym used to define the triggers or operations that will run or execute when monitors reach alarm levels. Monitors can be configured to perform certain tasks when they enter an alarm "state". These tasks are referred to as Alarm Actions.  

These four types of Alarm Actions are known together as the ATSE code. None of the ATSE Actions are required to apply an alarm. ATSE options can be applied during monitor configuration or at a later time. 

- **Alarm** - Creates Alarms within the Kaseya VSA.

- **Ticket** - Creates Tickets within Ticketing or Service Desk modules.

- **Script** - Runs a Script (Agent Procedure) on designated agents.

- **Email** - Sends Emails to designated recipients.

### Location and Impact 

The ATSE code can appear in several different monitoring sections as each monitor has the ability to configure a unique alarm action.

The ATSE code will always be located at the top of any page where monitors can be assigned to endpoints.

** Assigning Alarm Actions from the ATSE code can impact the Kaseya VSA, Clients, Agents, and Colleagues. **

#### Alarms

Applying alarms as an Alarm Action creates an alarm which can be found on the **Monitor > Alarm Summary** page.

Alarms will also show an Alarm State in the **Monitor > Dashboards** and will be logged in the **Agent Monitoring Logs > Alarms**. A new alarm will be created every time a machine enters or exits the alarm state.

If an alarm is not applied as an Alarm Action, there will be *no* records of the alarm in the Dashboard, Alarm Log, or Alarm Summary page.

Alarms can help quickly identify agents that require attention. However, excessive amounts of alarm creation can cause a negative impact on the performance of the Kaseya VSA.

#### Tickets

Applying the Create Ticket Alarm Action __will__ create a new ticket within Service Desk or Ticketing modules for every monitor that triggers an Alarm State.

Tickets __are not__ consolidated into one generic ticket every time a machine enters and exits an Alarm State.

Tickets will contain the alarm information that is specified in the Format Email option for the specific type of alarm.

Creating tickets for excessive or loud monitors can flood the Ticketing or Service Desk modules.

#### Scripts 
Running a Script or Agent Procedure after an Alarm State triggers is a very powerful alarm action. Desired scripts can be executed on the specific agent that triggers the alarm or another agent within the Kaseya VSA.

To assign a script to run, users must click the select agent procedure hyperlink and then choose an agent procedure that is accessible to this user. Then, a machine ID must be selected that will run the Agent Procedure. The machine executing the procedure must still be operational and checking into the VSA.

Assigning scripts can be implemented to remediate an issue, collect specific data from the agent at the time of the alarm, or verify if the machine is operating normally.

#### Emails 
- Selecting the Email Recipients option as an Alarm Action ***will*** send an email if checked and an alert condition is encountered to any email recipients assigned to the monitor.
- The Email address of the current user ***will always*** display in the Email Recipients field.
- The Format Email option allows the implementation of custom messaging and settings. 
- The "Add to Current List" option will add additional settings to an already applied monitor. This will update the email list on a monitor.
- The "Replace List" option will remove any previous email addresses and apply the newly specified emails.
- The "Remove" option will clear any email addresses assigned to a monitor without adjusting the monitor settings.

### Assigning ATSE to Agents 

You can assign ATSE to your agents via "Monitor > Agent Monitoring > Alerts". 

Choose the Alert Function from the dropdown menu and then select any of the ATSE Code boxes and machine(s) you'd like to apply them to. Then, click "Apply".

! To clear ATSE from any agent, simply select the agent(s) and click the **Clear** button.

### Event-based vs. State-based 

Kaseya has several methods of monitoring agents and assets. These methods involve using Microsoft Performance Monitor (PerfMon), WMI, SNMP, Event Logs, System Checks, and Log Monitors. 

These monitor tools can identify both Event-based Monitoring and State-based Monitoring.

**Event-based Monitors**

- **Alerts**: Fixed or agent-based alerts monitor events on agent machines. Fixed Alerts include Agent Status, Application Changes, Agent Procedure Failure, Get Files, Hardware Changes, Low Disk, Protection Violation, New Agent Installed, Patch Alert, Backup Alert, and System Alerts.

-**Event Log Alerts**: Event Log Alerts monitor Event Logs that generate in the Event Viewer on Windows Operating Systems. Event Log Alerts can generate an alarm for an event log, multiple event logs, or missing event logs. These alarms will only be triggered when an event does or does not get logged in the event viewer.

- **System Check**: System Checks monitor events on non-agent based machines from a designated agent within the Kaseya VSA. System Checks include DNS Server check, Port Connection check, Ping check, and Web Server check.

- **Log Monitoring**: Log Monitors track events in log files and alarm when they generate in a file or document. They will only trigger when certain events or keywords in a log are generated and then parsed correctly.

**State-based Monitors**

- **Monitor Sets**: A Monitor Set is a set of counter objects, counters, counter instances, services and processes that can monitor the performance of endpoints. Alarms can be set to trigger if a certain threshold or state in the monitor set is exceeded.

- **Monitors**: Monitors can collect various statistical data for reporting purposes. When a monitor test fails a specified number of times consecutively, the monitor enters an alarm state and executes a set of actions.

- **SMNP Monitors**: An SNMP Set or SNMP Monitor is a set of Management Information Base (MIB) Objects used to monitor the performance of SNMP enabled network devices. The SNMP protocol is primarily used to monitor agentless devices. Alarm thresholds or alarm states can be assigned to any object in an SNMP Set which will then trigger an alarm when the state or threshold is exceeded.

## Monitor Sets

### Overview

** Monitor Sets: Update Lists By Scan **

Monitor Sets are created using identified Perfmon Counters, Windows Services, and System Processes. Update Lists By Scan identifies the available objects and stores them in the Kaseya Database. 

The Lists are then available for viewing in the **Monitor > Edit > Monitor Lists** page.

#### Update Lists By Scan Q&A

**What does Update Lists By Scan do?**

Update Lists By Scan collects the latest available Counters, Services, and Event Log types on an individual machine.

** Why use Update List By Scan? **

Monitor Sets can be built off the populated Monitor List information. Using this procedure creates a more efficient process of populating Monitor Counters and Services within the Kaseya VSA to build monitor sets. If Update List By Scan is not run, no counters and services will be populated in the Kaseya VSA. This would then require manual creation for each counter, service, etc.

** When Should Update Lists By Scan be used? **

Update Lists By Scan is a very process-intensive procedure on the Kaseya Agent, the Kaseya Server, and the managed endpoint. Typically, only a handful of machines of each operating system type needs to be scanned to provide a set of comprehensive lists on the Monitor Lists page.

** How to run Update Lists By Scan? **

Update Lists By Scan is not recommended to run on a frequent basis. It should be run on for one-off scenarios or first-time use. Running Update Lists By Scan on many endpoints at once can overload the Kaseya Server. It is NOT recommended to run it on more than five machines concurrently.

### Creating Monitor Sets

Once Update Lists By Scan has been run, you can build Monitor Sets from the Monitor Lists. Monitor Sets give you the ability to define a group of counters, services, and processes to track endpoint performance.

An example **Monitor Set Tree**. All Kaseya VSA Users will have a Private folder to view and create their own individual monitor sets. You can create a new folder or select your default folder and create a new Monitor Set.

1. **Name, Description and Group Alarm**: A meaningful Name and Description can be assigned to a Monitor Set. You can also select the Group Alarm Column before clicking **Save**.
2. **Monitor Counters**: After clicking Save, you will be presented with the Monitor Counters. Click to **Add** one.
3. **Adding a Counter**: We will use this Monitor Set to monitor the C: Logical Disk and signal an alarm when it reaches below 10% disk space.
4. **Defining Criteria**: Work through the remaining steps 3-6 before saving your work.
5. **Saving the Monitor Set**: Lastly, click **Save** whenever you are done adding counters to the Monitor Set.

You've created a new Monitor Set. Feel free to edit, copy and/or export it as needed.

### Using Performance Monitor Counters

Performance Counters are available on supported Windows Microsoft Operating Systems. The Kaseya Agent leverages these Performance Counters to monitor endpoints.

Any Object, Counter, or Instance that exists within Microsoft PerfMon on a machine has the capability of being monitored. The Kaseya Agent will create PerfMon user-defined counters on the endpoint by implementing the logman command.

By clicking the **Counter Objects, Counters, and Counter Instances** buttons, list below it will update accordingly.

#### How does Kaseya use the Logman command?

Microsoft PerfMon Counters define specific monitoring information. The Logman Utility, used by the Kaseya Agent, creates these counters based on settings defined in the Kaseya VSA.

The agent will leverage logman commands and create counters for each monitor set. This data history will be distributed to the Kaseya Server for reviewing, analyzing, and alarming. On most Microsoft Operating Systems, there is a 64 counter limit for an endpoint.

Available counters can be found in Microsoft PerfMon on the endpoint, or using the `typeperf` command.

### Windows Services and Processes

#### Windows Services 

Monitor Sets can monitor any available Windows Services on an endpoint. Individual Windows Services can be specified or wildcards can be implemented to cover a group of services or all services that are set to automatic on a machine.

#### Windows Processes

Monitor Sets can track processes for various Operating Systems supported by the Kaseya Agent (Linux and MAC OS X Operating Systems). The specific process name must be listed - Update Lists By Scan can be added manually.

### Assigning Monitor Sets

Now that Monitor Sets have been created, they must be assigned to agents. The **Assign Monitoring** page allows monitor sets to be assigned to groups of machines. Note that *only one* monitor set can be assigned at a time. Groups of monitor sets can be applied using Policy Management.

Individualized Monitor Sets can be created to implement an independent monitor, or special circumstances monitor from a specific Monitor Set.

Select the Monitor Set for an assignment from the drop-down menu. Select the desired ATSE as well as the machine and click **Apply**. You will be prompted to confirm your selections. Click **OK**.

To remove a Monitor Set, simply select the agent(s) to remove it from and click "Clear".

## Fixed Alerts

### Overview

Fixed Alerts are Kaseya Agent-based alerts that run and trigger from the Kaseya Agent. The Agent will detect various changes depending on the alert and use built-in processes or triggers with the execution of an Audit.

The Kaseya Agent must be configured correctly for alarms to be triggered. Most but not all fixed alerts require the agent to be online and responsive.

#### "Monitor > Alerts" page:

- **Summary**:  The **Monitor > Alerts > Summary ** page will show all fixed alerts and event log alerts applied to a machine along with the ATSE code associated to each alert. This page provides a quick method to indentify what alerts are propagated to a machine.

- **Agent Status**: The **Agent Status** alert will alarm whenever the agen does not check-in to the Kaseya Server for the specified "Time Offline" It also has the ability to alarm when the agent comes back online and checks into the KSerer and alarm with a user disables Remote Control on the Agent.

- **Application Changes**: The **Application Changes** alert will detect adn alarm when an executable is moved, modified, added, or removed. This alert is dependant on audits running and will not trigger alarms without them.

- **Get Files**: The **Get Files** alert will alarm with a new versoin of a file specified in the **Agent Procedures > Get File** section is found.

- **Hardware Changes**: **Hardware Changes** alerts are dependent on Audit. If Audits do not run this alarm will not trigger. The Audit that detects the hardward is the System Information Audit.

- **Low Disk**: The **Low Disk** alert is based on an original Baseline and Latest Audits running to detect available free space on a machine.

- **Agent Procedure Violation**: **Agent Procedure Violation** alerts will trigger an alarm when any Agent Procedure fails in an applied machine. THere are no filters for this alarm, all agent procedures that fail will fire an alarm.

- **Protection Violation**: **Protection Violation** alerts will notify when any **Agent > Protection Settings** have been changed or detected.

- **New Agent Installed**: **New Agent Installed** alert will alarm whenever a new agent joins an applied Machine Group. This alert can only be applied to machine groups.

- **Patch Alert**: **Patch Alert** will notify when new patches are available, a patch install fails, agent credentials are invalid or missing, or WAU has chnaged. These alerts are dependent on Patch Scans to correctly trigger alarms.

- **Backup Alert**: **Backup Alerts** are only applicable for the **Backup Module** which implements Acronis backup tool. These alerts are on-demand and will trigger whenever the status completes in the backup module.

- **System**: These alerts are on-demand adn will trigger as soon as possible or the conditoin is met.

### Creating & Assigning Fixed Alerts

#### Creating & Assigning an Agent Status Alert

It's as simple as navigating to **Monitor > Alerts**, selecting the type of alert from the drop-down menu, defining ATSE and agent check-in criteria, and applying the alert to your machine(s).

#### Creating and Assigning an Application Changes Alert

Same as before, navigate to **Monitor > Alerts**, select the **Applications Changes** alert, configure the alert, and apply it to your machine(s) once it's ready to go.

### System Checks Alert

System Check Alerts allow for the monitoring of agentless devices. A Kaseya Agent in the VSA will perform the monitoring externally to this machine or device and report back the data received to the Kaseya VSA.

A system check typically determines whether an external system is available or not. Types of system checks include Web Server, DNS Server, Port Connection, Ping, and Custom.

#### Creating a Ping Check

You can set this up via **Monitor > External Monitoring > System Check**. Ensure to select **Ping** from the drop-down menu and fill out the rest. When done, simply apply the System Check to your machine(s).

#### Creating a Port Connection Check

Same as before, navigate to **Monitor > External Monitoring > System Check**, select **Port Connection** from the drop-down menu and fill out the rest. When done simply apply the System Check to your machine(s).

## Event Log Alerts

### Overview

Event Log Alerts allow you to monitor the Windows Event Log Viewer on any Windows endpoint within the VSA. 

An Event Set will be deployed to the monitored machine and then alert you when an event log entry for a selected machine matches specific criteria.

#### What is an Event Set?

Event Sets are defined parameters or a set of rules used to match against event logs that are generated. 

Each Event Set can have multiple rules or lines that will either be ignored or trigger an alarm. Event Sets must have defined rules or filters within them to match specific event logs. Filters must be matched exactly to the event log. Therefore, if a filter is entered incorrectly by just one character, digit, or space, the alarm will not be triggered.

! **Testing Event Sets**: It is recommended to test Event Sets prior to deployment to ensure they function correctly. Microsoft Windows has an `eventcreate` command allowing you to create generic or fake Event Logs within the Event Viewer. This can be used to test if Event Log Alerts are working or if a specific Event Set is working as designed.

#### Collecting Event Logs

Event Log Alerts are *not* dependent on collecting Event Logs in order to be triggered. 

Event Logs can be collected and stored within the **VSA in Agent > Event Log Settings**.

#### Why Collect Event Logs?

Collecting and retaining event logs within the Kaseya database will allow for event tracking, endpoint troubleshooting, and report execution. To review these event logs or report on them from the Kaseya VSA, they must be stored in the Kaseya Database.

#### What is an Event Log?

Event Logs are special files that record significant events on your computer, such as when a user logs on to the computer or when a program encounters an error. 

Whenever these types of events occur, Windows records the event in an event log that you can review later using the Event Viewer.

#### Why use Event Log Alerts?

- Event Log Alerts notify you on any event log that is generated on a machine. This can be a very powerful tool for debugging issues, preventing critical failures, or for tracking programs.

- Applications and Programs can create events within the event viewer to track progress, installations, and updates. Event Sets can be created to alert you and your technicians about these events as they are generated or completed.

- Event Logs can be used to diagnose critical failures on machines or alert you when the failure is happening on client machines. In most cases, when a hardware or software failure is occurring, it will generate errors or critical log types within the event viewer.

- Agent Procedures can leverage the "createEventLogEntry()" statement or the `eventcreate` command to track and log agent procedures.

#### The different parts of the "Assign Event Set" tab

- **Log Levels**: Every Event Log ***will*** have a certain log level associated - this log level dictates the severity and type of the log generated. A log level ***must*** be selected with Event Log Alerts are assigned to specify what log level should be alarmed on.

- **Alert Conditions**: Event Log Alerts can trigger under three different conditions:
	1. When an event occurs once.
	2. When multiple event occurs in a specified duration
	3. When an event does ***not*** occur.

- **Event Log Types**: Every Event Log will be generated in an specific event log type. The location of the Event Log that would like to be monitored should be selected. As an example if the Event Log is generated in the Application Log, the Application Log should be selected with the desired event set when applied.

- **Event Sets**: All created and pre-defined Event Sets are available in this drop-down menu. From here Event Sets can be edited, applied, and created.

### Creating & Assigning Event Log Alerts

Event Log Alerts can be created, assigned, and modified all from the same "Event Log Alerts" page. 

#### Create and assign an Event Log Alert for all errors.

Ensure that < **All Events** > is selected from the dropdown menu (Step 2), and **Error** is checked (Step 3). You can then set alert actions on the second tab if needed.

#### Create and assign multiple Event Log Alerts.

Ensure the values on Step 3 are changed from 1 to 3 and that the "time(s) within" is changed from **Day** to **Hr**.

#### Create an *Ignore* Event Log Alert.

Ensure to check the **Ignore** checkbox and click **Save**.

#### Remove an Event Log Alert.

Click the red X under the **Log Type** column and confirm the removal of the Event Log Alert.

#### Modify an Event Log Alert.

Click the **Edit** button (Step 1) to load the desired event set. Make sure you edit the filter, i.e. *Custom Event Set* > *Custom Error* (Step 4).

## Alarms

### Overview 

Once the Alarm action is enabled, it will create Alarm notifications in various locations within the Kaseya VSA. 

Alarms can be reviewed on the following pages: 

- Alarm Summary page
- Dashboards
- Alarm Log
- Monitor Action Log
- Notification Bar

#### Common Questions

**How do I know if Alarm Creation is enabled?** It may be necessary to review monitoring configurations to ensure an Alarm will be created. Assigned to each monitor configuration will be an ATSE code which will display if Alarms or the "A" is enabled.

**Why enable Alarms?** Enable Alarms to provide detailed feedback. Alarms allow monitor alerts to be reviewed in several locations such as the **Alarm Summary** page and in **Dashboards**.

**Are alarms required?** No, Alarms are not required for monitor alerts. Monitor actions will continue to operate even if Alarms are not enabled.

### Reviewing Alarms

#### Alarm Summary

The **Alarm Summary** page displays alarms for all machines that match the current filters. You can include additional filtering for listed alarms using fields in the **Alarm Filters** panel. You can also close alarms or re-open them and add notes to Alarms.

! Use filters to isolate certain alerts, individual alerts, or types of alerts. Wildcards (*) can also be implemented in the **Alarm Text** field.

#### Dashboards

Dashboards provide a visual display of data monitored within the Kaseya VSA. The **Dashboard List** page maintains configurable monitoring windows called **Dashboard Views**. 

Each dashboard contains one or more panes of monitoring data called **Dashlets**. Each VSA user can create their own customized dashboards.

#### Alarm Log

This log displays any alerts that have the Alarm action associated with the monitor. All alarm details will be included in this log.

The **Agent Logs** page. Navigate to **Agent Monitoring Logs > Alarms** tab to review the Alarm Log.

### Suspending Alarms

Alarms can be temporarily paused or stopped for maintenance or downtime. Suspending alarms can stop machines that are generating too many alarms due to hardware or software failures. Suspensions can also prevent a flood of alarms during maintenance periods and also stop unwanted alarm notifications to reach specific users or technicians.

#### Suspend Alarms

The Suspend Alarms action will prevent any monitor from triggering alert actions. This does not prevent the monitors from collecting data.

The **Monitor > Suspend Alarm** page allows you to suspend alarms on your agents

#### Suspend Agents

The Suspend action will stop all agent functionality such as Agent Procedures, monitoring, and patching without changing the agent’s settings.
The **Suspend/Resume** function inside the Agent module.

#### Disable All Alarms (On-Premise ONLY)
Disabling this setting prevents any alarms from generating on the Kaseya Server until it has been enabled. It is recommended to disable this setting during maintenance cycles.
The **System > Configure** page is only available to On-Premise Customers.


###Creating Dashboards Overview 

Reviewing monitor data can be a daunting task in terms of knowing where to look, what to check, and how to verify the issue. Dashboards greatly assist when reviewing monitor data and provide a single interface to review and monitor highlighted machines, machine groups, or organizations.

#### Common Questions

- **What are dashboards?**: Dashboards are visual tools that display real-time issues based on configured VSA data. Most dashboards consist of a single window with many different metrics displayed. A dashboard can empower a company with improved reporting, collaboration, integration, and user experience.

- **Why use dashboards?**: Historically, most companies switch between teams and coworkers using email communication, document sharing, and chat clients. Alternatively, dashboards can provide a single user interface where all team members can view new, current, or lingering issues immediately upon login to the Kaseya VSA.

- **What dashboards are available?**: Within the Kaseya VSA there are several dashboards, each one with a particular location:

	- The Monitor module has several dashboards available on the **Dashboard List** page. 
	- Network Monitor has its own dashboards located on the **Dashboard > View** page.
	- Info Center contains a **Management Dashboard** page with the complete status of endpoints.

- **What is the best way to utilize Dashboards?** A ***practical, functional***, and ***helpful*** dashboard design is a crucial component of a proactive business model. A well-defined, purposeful dashboard will greatly improve your efficiency. Here are some best practices for you to consider: 

	- Be clear on the purpose of the dashboard. Think about what you want to achieve as the purpose will inform the design.
	- Only include important data. Think about what data is crucial to supporting the purpose of the dashboard.
	- Be open to evolving your dashboard. Consistently check that your dashboard is serving its intended purpose and remains useful.

- **What is a Dashlet?**: In the classic Module, dashboards consist of one or many dashlets. A dashlet is a pre-configured dashboard view that can be adjusted to show certain organizations, machine groups, or machines.

### Creating a Dashboard

Monitoring dashboards are a great way to verify the status of configured monitors. Dashboards can be *shared* and *launched* on login to the VSA and then configured with desired alarms and endpoints.  

#### The different sections of the "Dashboard List" page:

- **Dashbord List**: This option allows new Dashboards to be created. The Dashboard created will be unique to your VSA user.
- **My Dashboards**: If checked, only the Dashboards you are the owner of display.
- **Grid**: All available Dashboards for the logged-on user will be present within this list. this includes shared Dashboards as well.
- **Load on Startup**: If checked, the Dashboard displays when the user log in. Choices apply ***only*** to the currently logged-in user. The Dashboard will appear as a pop-up.

#### The Dashboard List page maintains configurable monitoring windows called Dashboards Views. Each VSA user can create their own customized dashboard. 

**Monitor Dashboards** The **Dashboard List** page is the VSA's primary method of visually displaying monitoring data, including alerts and alarms.
1. **New Dashboard** Click the plus icon (+) to create a new Dashboard View. The new dashboard displays in a popup window. 
2. **Title and Description** Enter a Title and Description for your new dashboard and click on **Add Dashlets**.
3. **Dashlets** Select all desired checkboxes and then click the **Add** button. Close the **Add Dashlets** menu.
4. **Configuring Dashlet** You can move and resize the dashlets within the **Dashboard View**. You can also edit the dashlet and set machine online criteria.
5. **Saving the Dashboard** Lastly, save your dashboard and go back to the Dashboard List page to see your newly created dashboard.

! You can delete the dashboard by clicking the red "x" icon in the **Dashboard List** page. You can edit it if needed, create a copy of the dashboard, and set it to load on VSA startup.

## Introduction to Policy Management

### Overview

Consistency is the hallmark of an effective, agile organization. With thousands of moving parts, managing every user and every system consistently is critical.

Kaseya Policy Management streamlines the process of creating, setting, and remotely applying IT policies to groups of systems across a distributed organization. You can view all policies from a single web-based dashboard, customize, and assign them based on Organization, Machine Group, machine type, platform, or any dynamic view of machines. This ensures all systems are in compliance.

The **Policy Management > Overview** page

#### Key Terminology

- **Cabinet** - The highest-level container in a folder tree. Within the Policy Management module, the Cabinets are **Policies** and **System**. The Policies cabinet is used to organize custom policies and the System cabinet is populated with policies from Kaseya after enabling the System Management utility.

- **Folder** - Organizational structures within a Cabinet. Folders can be nested to create parent and child-level folders for additional structure.

- **Policy** - Policies are a group of defined settings. Most agent-related settings available throughout the VSA can be defined within a policy.

- **Policy Object** - A single setting group within a policy. Policy Objects align with various agent settings throughout the VSA. 

- **View** - Views used by Policy Management are exactly the same as the Views used to filter the machine list throughout the VSA. Within Policy Management, Views are used to determine which machines should receive specific policies where each policy is associated with a View.


### Policy Management Settings

Policy Management schedules **must be** configured to ensure proper application of settings to managed machines. Employing regular checks verify compliance with the assigned policies. Explore the options below to learn more about the functions of these schedules.

#### Settings

To access the Deployment Interval and Compliance Check schedules, navigate to the **Settings** page of the Policy Management module.

- **Deployment Interval** - As new machines appear or their existing associations are changed, policies may need to be deployed or re-deployed. The frequency of this process is configured using the Deployment Interval. Setting the deployment interval to "Manual" requires the user to click the **Apply Now** button on the **Policies** page to deploy a policy.  The deployment interval also consumes the Override notification when policy-managed settings are changed directly via a module page.

- **Compliance Check** - The Compliance Check schedule defines how often Policy Management will compare the settings configured in assigned policies that are actually applied to managed machines. When all settings match, the machine is considered "In Compliance". If any settings vary, the machine is marked as "Out of Compliance". If the Compliance Check schedule is not configured, Policy Management will not run processes to compare settings.

### Creating Custom Policies
The **Policies** page allows you to create a policy folder via the **+Add Folder** button or by right-clicking the cabinet.

Policies can *only* exist inside of a policy folder and *cannot* be created directly inside a cabinet. By default, the cabinets will exist, but will not contain any folders. 

You must create *at least one* folder inside the Policies cabinet before a custom policy can be built. Once the folder is created, select the folder and click the **Add Policy** button.

**Once the policy is created, the settings can be defined. Selecting the policy from the folder list will display the policy settings to the right.**

Edit the policy's name, add a description, and associate the policy with a View

! A View must be defined.  If no View is defined, the policy will be ignored when assigned to a Machine Group or Organization. Policies without a defined View can be assigned directly to an individual machine.

**With the Credential object, define a fixed credential by entering a username and password.**

Multiple Policy Objects can be included in the policy. Once all desired Policy Objects are added and configured, feel free to click **Save** or **Save and Apply**.

! By choosing the "Use Manage Credentials from Audit Menu" option above, the same policy can be used by multiple clients, even if the credential varies between each client. 

**"Save" & "Save and Apply"**

After making any changes to a Policy, the changes *must* be saved. Saving the changes will not immediately cause the settings to populate to managed machines. For the settings to populate to assigned machines, the policy must also be applied. 

- **Save** - This will commit the changes to the database in a field marked as pending. These settings are stored, but they will not be populated to any machines assigned to the saved policy. 

- **Save and Apply** - This is the same as clicking **Save** and **Apply Policies**. Use this option in smaller environments such as when a policy is assigned to a limited subgroup of machines, or when the settings need to populate to the managed machines quickly. After clicking **Save and Apply**, you will be prompted to Apply Now or Allow Scheduler to Apply.

! Selecting **Apply Now** from the dialogue will immediately deploy the defined settings to any machines associated with this policy. If you are creating a new policy, it is not yet assigned to any machines and, therefore, no settings will be populated. However, as soon as the policy is assigned to a Group, Organization, or individual machine, the settings will populate to the managed machines.

### Policy Precedence

#### Key Terminology

- **Compliance** - A background process. Compliance Checks run periodically to determine if the settings defined in assigned policies are actually applied to the appropriate endpoints. Agents are either "In Compliance" or "Out of Compliance". Icons identify the current status of each managed machine.

- **Manual Override** - An Override occurs when Policy has been configured to manage settings for an agent but the settings are changed outside of Policy Management.

- **Policy Precedence** - Multiple policies can be assigned to individual machines. In many cases, there will be policy objects across these policies that conflict with each other. 

- **Conflicting Policy Objects** - Multiple policies can be assigned to managed machines. In the event of settings conflicts between co-assigned policies, Precedence Rules will determine which settings will be applied to the managed machine.

- **Combining Policy Objects** - While most policy object types will conflict when two policies assigned to a single machine include the same settings, there are a few object types that will combine. While a machine can only have a single Working Directory, multiple Agent Procedures and Monitor sets can be assigned to a single machine. In the event two policies define a Combining policy object type, the assigned machine will receive the settings from all policies.

#### Understanding Combining Objects

Policy A defines two Agent Procedures and Policy B defines two different Agent Procedures. Both policies are assigned to the same endpoint: "workstation-1".

If the same procedure is scheduled in both policies and each with a different schedule, policy precedence rules will determine which procedure schedule will be applied to the endpoint. For combinable objects, Policy Management will use the same logic as the module. If the module allows the same object to be assigned multiple times to the same endpoint, all settings from all associated policies will be passed to the endpoint. If the module allows only one setting per machine for the selected object, policy precedent rules will be followed.

! Policy Objects that combine include Monitor Sets, Agent Procedures, Event Log Alerts, Distribute Files, and Alerts.

#### Understanding Conflicting Objects

All remaining policy objects conflict. When a conflict exists, the winning object is determined by precedence rules. The more closely a policy is assigned to a machine level, the more precedence the policy has.

The assignment layers are as follows:

- **Global**: A policy assigned at the Global layer will apply to all managed machines, regardless of Organization or Machine Group membership.
- **Organization**: A policy applied at the Organization layer will apply to all managed machines within the Organization. Any conflicting Global layer objects will be overwritten with the settings in policies applied at the Organization layer.
- **Parent Machine Group**: A policy applied at the Parent Machine Group layer will apply to all managed machines in the Machine Group, including any child-layer Machine Groups. Any conflicting objects applied at the Global or Organization layer will be overwritten with settings from the policies applied at the Parent Machine Group layer.
- **Machine**: Policies assigned directly to a managed machine will proceed over any conflicting settings from all higher layers. Policies with no View defined can be assigned directly to a machine and the settings in that policy will be applied.
- **Child Machine Group**: Policies assigned at a Child Machine Group layer will overwrite any conflicts from policies assigned at the Global, Organization, or Parent Machine Group layers.

### Assigning Policies

Building the policy, even with a View associated, will not cause the settings to deploy to agents. Once policies have been built, they must be assigned for the settings to populate to managed machines.  

When policies are assigned to Global, Organization, or Machine Group levels, the view associated with the policy will dictate which member machines will receive the policy.

Organizations and Machine Groups are listed in the center of the page. Simply click and drag the individual policy from the Policies list to the appropriate Organization or Machine Group.

! Policies with no View assigned will appear with a red scroll icon in this list. Any settings in these policies will be ignored if the policy is assigned to an Organization or Machine Group.

#### Facts

- Any policies assigned to the Global Organization will apply to all managed machines, regardless of organization, or machine group. Global Organization policies have the least amount of precedence.

- Policies can be applied to the "unnamed" Organization. This can be beneficial when the agent package directs new agents to check into the unnamed group initially. You can schedule first-run processes on these machines prior to moving them into the permanent Machine Group.

- An entire folder can be assigned to an Organization or Machine Group. When a folder is assigned, all policies within the folder are assigned. If new policies are added to the folder, they will automatically be assigned to the Organization or Machine Group.

- When an entire folder is assigned to an Organization or Machine Group, the precedence of the policies within the folder is based on the order in which the policies appear in the folder. The higher in the folder, the more precedence the policy has.

- The policies in each folder have precedence within the folder based on where they appear in the list. The list can be re-ordered by dragging policies to a different position in the list.

- You can dictate which settings should take precedence in the event of a conflict. By re-ordering policies within a folder, if there are conflicts between the policies in the same folder, and if that folder is assigned to an organization or machine group, the settings will apply to managed machines based on the order of the policies as they appear within a folder list. 

#### Assigning by Machine

While assigning policies by Organization and Machine Group is the preferred automated method for configuring Agent settings, there are cases where it may be necessary to assign a policy directly to an individual machine. You can do so via the **Policy Management > Assignment > Machines** page.

You can assign policies to individual machines via this page. Remember that policies can still be assigned directly to an individual machine even if the policy does not have a View defined.

! Policies assigned directly to a machine have more precedence than any other assigned policy. Where conflicts exist, the settings defined in the machine-assigned policy will take precedence.

#### Assigning Multiple Policies by Machine

Multiple policies can be assigned directly to individual machines. When multiple policies are assigned, it may be necessary to re-order policies to ensure policy precedence assigns settings appropriately. The higher in the list, the higher the precedence.

Move policies up and down, or remove them from machines by leveraging these buttons.

### Policy Compliance

Once policies have been assigned, the settings defined within the policies will first be marked for and then deployed to the appropriate agents. Policies as a whole will be marked as either in or out of compliance. 

This is indicated by the policy status icon on the **Machines** function of the **Policy Management Module**. There are several potential status icons, but in and out of compliance icons are the most common.

Green = In compliance
Red = Out of compliance
Yellow = Marked for Deployment
Orange = Override
Black = No Policy Attached

! The Compliance Check process runs on a pre-determined schedule based on the **Settings** page of the **Policy Management** module. Schedule the Compliance Check to run on a recurring basis, generally *no more frequently than once per day*.

## Introduction to Software Management

### Overview

**Software Management** manages the deployment of popular third-party software packages for both Windows and Apple operating systems. 

This module is also able to carry out patching for and deployment of some third-party software though this additional functionality is separately licensed.

#### Software Management Module

- **Management**: The **Management** page acts as the control center of the module, providing you with a number of tools designed to assist in viewing metrics related to patching and current endpoint vulnerabilities.
- **Profiles**: A **Profile** can be thought of as a set of instructions or rules through which different threats to endpoints can be identified, filtered, and removed. 
- **Configuration**: From the **Configuration** page, you can set general options for the entire module. Perhaps most significantly, it is from this function that you can prevent Software Management and Patch Management from running concurrently. Additionally, you can migrate Knowledge Base overrides and policies from Patch Management.
- **Administration**: The primary role of the **Administration** page is application logging. The **Application Logging** page displays a log of Software Management module activity using the following convenient identifiers: Event Name, Message, Admin, and Event Date.

### Scan & Analysis

You must be able to ensure that your team can properly identify vulnerabilities on endpoints and, when needed, patch those vulnerabilities. To do this, you will need to create a **Scan and Analysis Profile**. 

System and network security depends on all of your machines having the latest security patches applied. Using the **Scan and Analysis profile** allows you to schedule patch scans and to approve, review, or reject patches based on the endpoint’s assigned profile.

The **Scan and Analysis** page allows you to create new profiles, edit existing ones, and delete them as needed. Once you click **Save**, confirm whether or not you want the profile created

! We recommend that you follow a Patch Impact configuration similar to the one above. Critical Updates and Virus Removal should under most circumstances be *Approved*. You may want to Review Recommended updates on a case-by-case basis,  and *Reject* updates older than 30 days. 

#### You will then see your new Scan and Analysis Profile appear in the “Profile Name” column. 

**Scan and Analysis** profile we just created. All of the selections that you made during profile creation are reflected on the right-hand side of the screen.

### Deployment

Now that you have created the Scan and Analysis Profile, you will need to create a Deployment Profile next. 

The **Deployment Profile** page helps you create profiles that specify how and when deployments are executed on assigned machines. The Deployment Profile can be assigned on the page shown next, or on the **Machines** page.

The **Deployment** page showing the "Add Deployment" window with a sample configuration. Once you click **Save**, confirm whether or not you want the profile created.

#### Additional Reboot Options:

Other options are available to select from in the first two drop-down menus.

! Agent Procedures can be run before *and* after updates. For example, you might want to stop services before a reboot and check to ensure that they have restarted after reboot.

It is also wise to schedule deployments only during hours when employees are not using the servers. Coordinating patch deployment with off-peak hours helps your company avoid the disruption of crucial tasks. Additionally, setting a blackout window for business-critical servers during known business hours will prevent servers from being rebooted.   

#### You will then see your new Deployment Profile appear in the “Profile Name” column. 

An example Deployment profile. All of the selections made during profile creation are reflected on the right-hand side of the screen.

### Override

For some users or endpoints, exceptions to the Scan and Analysis Profile must occasionally be made. Approve, Deny, and Review rules are set from within the Scan and Analysis Profile.

Then, the **Override Profile** allows you to create overrides that have precedence over a Scan and Analysis or 3rd-party Software Profiles assigned to a given machine. 

The Override page allows you to specify named sets of selected overrides.

! **Note**: The "KB Overrides" and "Patch Overrides" tabs are no longer supported however, we have retained your historical data and provided you a migration path for your overrides.

#### Overrides

To create a new override, simply click the **+New** button and search in the rows or add additional ones by clicking on **+Add Row**.

The "New Override" window allows you to add multiple rows and set it to Approve/Reject/Review/Suppress. Alternatively, you can delete rows as needed.

### 3rd-Party Software

The **3rd-Party Software** page allows you to assign software titles to a profile by a version number. Software titles are deployed based on the schedule specified by a machine’s assigned Deployment Profile. 

The 3rd-Party Software page allows you to create, edit, and delete profiles.

#### Adding Multiple vs. Individual Titles

- When creating your 3rd-Party profiles, make sure to use profile names that will assist you in quickly recognizing the software in question. It’s also a good idea to include a brief description of the software although it is not required. 

- The "Software" portion of the page, allows you to view all vital specifics about the 3rd-Party Software affected by the policy.

- The **Add Multiple Titles** and **Add Individual Titles** buttons allow you to add software on demand.

Adding multiple vs. individual titles. Click **Add** after locating the software you're looking for and click **Save** to save the profile

#### You will then see your new 3rd-Party Software Profile appear in the “Name” column. 

Example of **3rd-Party Software** profile. All of the selections made during profile creation are reflected on the right-hand side of the screen.

### Alerting

The **Alerting** page controls Software Management Alert Profiles. Each Alert Profile represents a different set of alert conditions and the alert actions that will occur in response to that alert.

Multiple Alert Profiles can be assigned to an endpoint. It is important to note that changes to an alert profile will affect all Machine IDs assigned to that profile. 

The **Alerting** page allows you to create, edit, delete, and copy profiles as well as set Alerts Configuration.

#### Summary

From the **Summary** tab, you can view and set basic options for Alert Profiles, such as "Name" and "Description". 

The **De-duplication** option enables you to prevent the generation of duplicate alerts. Alerts can be organized by patch or by machine and can be set up to suppress duplicate alerts over a number of specified time frames (Days, Hours, Minutes).

The **Alert Profile > Summary** tab

! Always make certain that your profile names and their corresponding descriptions are clear and accurate. Alerts can be generated based on a number of conditions so, it is recommended that you note specific alert conditions. An example of a condition would be a failed patch deployment. 

#### Alert Types

Within the **Alert Types** tab, you can customize the conditions that trigger the creation of a Software Management Alert. For example, imagine a critical patch failed during deployment. Receiving notice of such a failure is crucial for you; hence, the importance of alerting.

The **Alert Profile > Alert Types** tab

! You can choose for alerts to populate when a new patch is available when a deployment fails, and/or when an OS Auto Update has changed. 

#### Actions

If the **Create Alarm** or **Create Ticket** checkboxes are checked and an alert is encountered, tickets and/or alarms will be created, notifying selected users of any issues indicated within the **Alert Types* tab.

The **Alert Profile > Actions** tab

! You can anticipate alert conditions and prepare your endpoints by pre-selecting an agent procedure. If you enter the agent procedure into the "**Script Name to Run**:" box, the procedure will run post-update. 

#### Endpoints

The **Endpoints** tab allows you to view all endpoints assigned to the selected Alerts Profile. To add a new machine to your Alerting Profile, simply click the **+Add** button, select the desired endpoint, and click **Save**

The **Alert Profile > Endpoints** tab.

### Assigning Profiles

You have the ability to assign profiles to each managed machine so that they can approve, reject, or review patches based on their classification. This way, they can meet both technical and customer requirements for approving and denying updates.

You can navigate to the **Machines** page to select your machine(s). From there, click on **Assign Profiles**.

#### Assigning Profiles

The Software Management profiles we created can be selected from the three drop-down menus. Confirm that everything is correct and then click **Assign**.

From the "Machines" tab, you can see the various profiles to which an endpoint or Machine Group has been assigned.

### Manual Scan

The **Software Management** module also provides you with the option to conduct a Manual Scan and Deployment on selected endpoints. If an endpoint requires a scan or deployment prior to the scheduled maintenance, you can conduct a Manual Scan. To do this, simply navigate to the **Machines** function in Software Management. 

The **Machines** page manages the assignment of Software Management profiles on selected machines. Once a scan has been performed, values for the above categories will appear, reflecting the results of the scan.

! The Force Update button on this page should only be used with the utmost care. Once selected, reboot options are ignored and the managed machine(s) will reboot *without* warning the user as often as necessary until the machine has been brought into compliance. 

#### After conducting your Manual Scan, you may want to deploy patches. To do so, simply click on the desired vulnerability and choose the option Deploy Patches.

You can select the vulnerability of your choice and click the **Deploy Patches** button or you can just right-click on the vulnerability and select one of the other options.

### Patch Approval and Vulnerabilities

Patches set to "Review" in the Scan and Analysis Profile must be checked and approved. Both the **Patch Approval** and **Vulnerabilities** pages in Software Management allow you to review and approve patching for specific security risks associated with a managed endpoint. 

In addition, both the **Dashboard** and **Patch History** pages can assist you in reviewing and assessing endpoint risk. Let's go over these four pages next!

#### Patch Approval

This page allows you to identify patches by any of the helpful classifications below: Vendor, Product, Patch Name, or Release Date. 

From the **Patch Approval** page, you can either Approve or Reject patches previously set to review. 

#### Vulnerabilities

The **Vulnerabilities** page lists the vulnerabilities discovered on all scanned machines in the VSA. Vulnerabilities are security risks associated with a machine and can include OS configuration, applications, firewall settings, browser plugins/extensions, antivirus and malware support, removable devices, scripts, and macros.

You can see vulnerabilities by clicking on the **Vulnerabilities** page or from within the **Machines page > Vulnerabilities tab**.

! To remove a vulnerability by deploying a patch, simply click on the vulnerability, and then select **Deploy Patches**.

#### Patch History

The **Patch History** page is a helpful tool for viewing the history of all approved and rejected patches for a selected profile. Here, you can select the hyperlink of a listed patch to view its details.

- **Installed Patches** - Allows you to view what patches have been installed per machine basis.

- **Rejected Patches** - Allows you to view what patches have been rejected and approve them from within the tab if needed.

- **Suppressed Patches** - Allows you to view what patches have been suppressed and approve them from within the tab if needed.

The **Patch History** page has three different tabs: Installed Patches, Rejected Patches, Suppressed Patches

! The **gear icon** on the right-hand side allows you to export the selected profile's patch history, refresh the list, as well as clear any filtering set for the list.

#### Leveraging Views

You should now be familiar with VSA Views from the previous Course, "Remediation". 

You can set up Views and apply the following filters/criteria for patches.

#### Dashboard

The **Dashboard** page provides a comprehensive view of Software Management metrics and activities. 

### Configuration Settings

The **Settings** page lets you configure options for the entire Software Management module in two tabs: *Application Settings* and *Migration*. 

#### Application Settings 
- **Edit Button**: You can click the **Edit** button to change the settings you see here. You can read more about it in the help documentation.
- **Reboot Action Email**: If you selected *"Do not reboot after update, send email"* in the Deployment Profile you will receive the **Reboot Action Email**, which will inform you which machine requires rebooting;
- **Compliance**: 

	- **Compliance Check** specifies how often machiens are checked for compliance
	- **Scan and Deploy Grace Periods** specifies the grace period included in compliance checking for both scan and deployment. A machine is considered out of compliance if at the time compliance is checked the last actual scan or deployment was later than the last schedulded scan or deployment plus the listed grace period.
	- **Patch Tolerance**: specifies a percentage ratio of deployed patches to approved patches. A machine is out of compliance if deployed patches are less than the specified precentage of approved patches. 

- **Vunerablility Definition** specifies whether to ***include*** or ***exclude*** suppresed patches. This option reflects on the entire module experience.

- **Migration**: If checked, Software Management ***will not*** run **Scan Now** on an agent if that agent is configured to use any of the Patch Management features:

	- Patch Management Policy
	- Scan Schedule
	- Automatic Update Schedule
	- Machine Update Schedule
	- Patch Update Schedule

- **Settings**

	- **Private Profiles** if checked, profiles are only visible if the profile was created by you or if the profile is assigned to a machine assigned to the scope you are using. Profiles are public by default.
	- **Enable Native Kaseya Engines (BETA)** if checked, Windows 3rd-party installers will be deployed from Kaseya Catalog (the #K3PP Software Catalog" page will be visible under your Software Management module). You will need to allow *** 15-20 minutes*** for Engines synchrozination process to complete. Note, this is a one-time only technical event. 
	- **Display Third Party Vulnerabilities** This historical function has been elevated to include the following options and behaviors as a result"

		- **Hide All** if selected, Third-Party patches will ***not*** be included in scans and deployments.
		- **Hybrid** (Default/Recommeded Option) if selected, Third-Party Patches will ***only*** be included in scans and deployments on agents with Third-Party Support Enabled.
		- **Show All** if selected, this lastest function ***will*** list all third party patches available for deployment on endpoint(s) without the need to enable or be licenced for third party updates.

#### Migration Tab

Under this tab you can click on the **Migrate Knowledge Base Overrides** and **Migrate Policies** buttons to learn more about these processes.

___________________________________________________

Q: What does ATSE stand for?
A: Alarm, Ticket, Script, Email

Q: Select all that apply: What are the methods Kaseya uses for monitoring agents and assets?
A: Microsoft Performance Monitor (PerfMon), WMI, SNMP, Event Logs, System Checks, and Log Monitors

Q: True or False: Monitor Sets are created using identified Perfmon Counters, Windows Services, and System Processes.
A: True

Q: What function does "Update Lists By Scan" perform?
A: Collects the latest available Counters, Services, Processes, and Event Log types on an individual machine.

Q: True or False: It is not recommended to test Event Sets prior to deployment.
A: False

Q: True or False: Once the Alarm action is enabled, it will create Alarm notifications in various locations within the Kaseya VSA.
A: True

Q: True or False: Policy Management schedules must be configured to ensure proper application of settings to managed machines.
A: True

Q: Policies can only exist inside of a policy folder and cannot be created directly inside a cabinet.
A: True

Q: Select all that apply: Select the profiles found in the Software Management module within the VSA.
A: Scan and Analysis Profile, Overide, 3rd-Party Software, Deployment, Alerting

Q: True or False: You have the ability to assign profiles to each managed machine to approve, reject, or review patches based on their classification. 
A: True
