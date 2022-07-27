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

- **Application Changes**: The ""Application Changes** alert will detect adn alarm when an executable is moved, modified, added, or removed. This alert is dependant on audits running and will not trigger alarms without them.

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











