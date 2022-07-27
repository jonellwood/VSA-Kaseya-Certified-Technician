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

** Emails **
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









