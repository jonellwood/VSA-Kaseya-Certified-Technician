# Remediation #

## Audit Information ##

### How are Audits Useful? ###

Audits help you to gain insight and knowledge of inventory, devices, hardware, software, configurations, licenses, network settings, and connected devices.

Audits allow easy management of machine equipment and software in an environment. They will keep a baseline record of all machines and have the ability to alert on any changes performed to managed machines from a software or hardware point of view. 

*Example of Audit Information*

- All Hardware - Such as CPUs, RAM, PCI Cards, and Disk Drives.
- All Installed Software - Such as Licenses, Version Numbers, Full Paths, and Descriptions.
- System Information from DMI and SMBIOS - Such as PC make, model, serial number, motherboard type, and any other detected BIOS information.
- Current Network Settings - Such as Local IP address, Connection Gateway IP address, DNS, WINS, DHCP, and MAC address.

### Types of Audits ###

To see the different types of audits available, navigate to **Audit > Collect Data > Run Audit > Run Audit Now** in the side menu

- **Baseline Audit** - Review and assess the system in its original state. Typically, a Baseline Audit is performed when the Kaseya Agent is first installed.
- **Latest Audit** - Review the configuration of the system as of the last audit ran and compare results from that last original baseline.
- **System Information Audit** - Collect all DMI/SMBIOS system data as of the last System Information Audit ran.

! **Frequency of Audits:**

- Baseline Audits should be run or scheduled for annual execution. 
- Latest Audits should be scheduled on a more frequent basis to detect recent changes on machines. Once a week is recommended. 
- System Information audits should be executed during the initial installation of the agent and only require additional executions after any hardware changes.

### Running/Scheduling Audits ###

**Audits can be scheduled to run on a recurring basis or executed on demand.**

### Reviewing Audit Information ###

To view audit information per machine, navigate to "Audit > View Individual Data > Machine Summary", select the agent from the list, and click on the available tabs.

The **Machine Summary** page shows you audit information for a single machine at a time.

! The various tabs shown below allow you to select the type of audit information you'd like to review for a single machine. The tabs available are **Software, Hardware, Agent Information, Patch Status, Remote Control, Documents** and **Users** of the specific machine. When clicking each tab, sub-tabs will then display.

### Manually Editing Machine Data ###

If needed, you can manually edit machine data for System Info Audits. 

To do so, select the agent you'd like to edit the data on and click the "Edit Machine Data" button.

The pop-up you will receive when clicking the **Edit Machine Data** button. Here, you can manually edit audit fields.

! You will also be able to enter data for Custom Fields which we will cover in an upcoming lesson.

### Installed Applications ###

The "Installed Applications" page lists all applications found during the Latest Audit for a selected agent.

The **Installed Applications** page showing installed applications for the selected agent.

! You can filter out by any of the given columns. Simply click on the "down" arrow, go to **Filters** and type the Application, Description, Version string, etc.

### Add/Remove ###

The "Add/Remove" page displays the programs listed in the Programs and Features window of the managed machine. The information shown on this page is collected when a Latest Audit is performed. 

The **Add/Remove** page showing installed software for the selected agent

! You can leverage the **Uninstall String** column to reference the string you'd use for uninstalling the software from the managed machine.

## Custom Fields ##

### Overview ###

The Kaseya VSA automatically collects data regarding each managed machine through the audit process you learned about in the previous lesson. However, there is some information you may want to track and report on that is not automatically collected by Kaseya. This is when Custom Fields come in handy!

### Creating Custom Fields ###

You can maintain an unlimited amount of Custom Fields information about managed machines. They are supported in Views, Agent Procedures, and Reports. However, note that custom reports *do not* support more than 100 custom fields. 

You can create, rename, and delete Custom Fields via the **Machine Summary** page.

Custom Fields button can be located in **Audit > View Individual Data > Machine Summary**.

### Types of Custom Fields ###

**String** - Used for text-based data.
**Number** - Used for numerical data. If your field requires text and numerical entries, choose the String data type.
**Date Time** - Used for cases where both the date and the time are required for tracking in a single custom field. Data will display in HH:MM:SS MM/DD/YYYY format.
**Date** - Used when the data will track a specific date. Data will display in MM/DD/YYYY format.
**Time** - Used when the data will track a specific time without reference to a date. Data will display in HH:MM:SS format.

! When using the **Date Time** and **Date** data types, the time zone of the VSA Administrator/Technician can impact the date they see as the value for the Custom Field. 

### Defining Custom Fields Data ###

As you learned in previous lessons, you can manually edit machine data for System Info Audits and Custom Fields also. Click the "Edit Machine Data" button to do so.

This edit pop-up window allows you to edit any of the Machine Data collected by the System Audit as well as the data for any Custom Fields.

! Rather than having to manually enter the data for the desired Custom Field, use Agent Procedures to populate Custom Fields via the **updateSystemInfo** step. More details can be found within this KB article and Agent Procedures will be covered in an upcoming lesson.

### Bulk Editing Custom Fields ###

In some cases, you may want to enter the same data value into a Custom Field for several machines at once. This is possible via the **Bulk Edit Custom** button.

Select the desired agents and click the **Bulk Edit Custom** button when you're ready to bulk update a Custom Field.

When a Custom Field is selected from the drop-down menu, you can either re-use a value used on other machines or update the value. When ready, click the **Save** button.

### Renaming and Deleting Custom Fields ###

Renaming a Custom Field is as simple as clicking the "Rename Custom Field" button and selecting the field to be renamed.

The **Rename Custom Field** pop-up window will allow you to rename a Custom Field of your choice. When done, click the **Rename** button for the changes to take effect.

The data assigned to the individual machines is preserved. The data type can *only* be defined at the time of creation of the Custom Field. Once defined, the data type *cannot* be changed.

You can delete a Custom Field by clicking the "Delete Custom Field" button and selecting the field to be deleted.

The **Delete Custom Field** pop-up window will allow you to delete a Custom Field of your choice. When done, click the **Delete** button to complete the action.

! **All data contained in the Custom Field for any machine is lost.**

## Audit Manage Credentials ##

### Overview ###
With the Managed Credentials function, you can configure multiple credentials for documentation purposes, create new local credentials on the managed endpoint, and assign credentials for usage in the Kaseya VSA. 

The credentials can be configured on an Organizational, Machine Group, or an individual agent level. Comparatively, the Set Credentials function allows you to set a pre-existing credential that will be used in the Kaseya VSA on an individual basis.

### Best Practices ###

- Use Managed Credentials to have one location to store credentials for all assets and devices.
- Use passwords that meet the required environmental complexity.
- Stay within limits. For example, Windows XP machines have a 10-character password limit.
- Generally, set managed credentials on the Organization or Machine Group level. Set the managed credentials on the individual endpoint as the *exception* rather than the rule.

### Creating Managed Credentials ###

Managed Credentials can be used to create, delete, and view credentials for Organizations, Machine Groups, and individual Machines to organize access rights to machines. 

For each credential, the username and password can be set. A domain name can *optionally* be configured, and finally, the credential can be set for use as the agent credential for the endpoint(s). 

**Description** - A one-line description for the credential. Use this optional field to quickly understand the use cases for the Managed Credentials.

**Username / Password / Domain** - Enter the username and password for the Managed Credentials and a domain if applicable.

**Set as Agent Credential** - This option registers the credential required by an agent to perform user-level tasks on a managed machine. *Only one* credential for this Organization or Machine Group can be designated as the source credential for an agent credential. 

**Notes** - *Optionally*, include a note with the credential. Notes is useful for adding in more details to the use case(s) for the Managed Credentials. It can also be used to note additional information regarding the permission levels of the managed credentials for other administrators or technicians.

Once the Managed Credential is in place, the Organization, Machine Group(s), and Machine(s) are populated with a key indicating credentials are specified for the row where it appears.

! You can edit the credentials at any time (**Edit** button), view them (**View** button) which will reveal the password, and/or delete them (**Delete** button).

### Reviewing Credential Logs ###

The Credential Log page provides an audit log of the VSA users who create, modify, and delete credentials on the "Audit > View Assets" and "Manage Credentials" pages.

Use the **Credential Log** page to view all activities that have occurred under each credential to determine if any modifications have been made by a Kaseya user. It can also help review a variety of other information including which users are accessing the system at certain times of the day.

## View Assets ##

### Overview ###

An asset is *any device* within an environment or network. There are two types of assets in the environment: a managed asset and a non-managed asset.

### Types of Assets ###

- **Managed Assets**: Computers and mobile devices that have an agent installed on them are always considered *managed assets* and display on the **View Assets** page for as long as the agent is installed.

- **Non-Managed Assets**: When an agent cannot be installed on a discovered device, the device can still be "promoted" to a managed asset and display on this page. For example, a router or printer may still require monitoring, even if an agent cannot be installed on the machine.

Example assets under **Audit > Asset > View Assets**.

### Viewing Assets ###

The **View Assets** page provides a detailed list of functionality enabled on an asset. This page is populated by Discovery scans of *networks* and *domains*. Here, you can view assets, demote them, change their group, and refresh the grid.
 
- **View**: Displays a popup window of informatoin about a selecte device. Different views, base on the type of prove used ot collect the information, can be selecte using the Probe Type drop-down list: NMAP Probe, Machine Audit, vPro and Merge View.

-**Demote Assett to Device**: Removes a selected device as managed assett - computers and mobile devices that have agents installed on them can not be demoted.

-**Change Group**: Changes the Organizatoin and Machine Group assigned to the asset

-**Refresh**: Refreshes the View Assets grid which diplays all known information on the available assets. Columns can be added, removed, and sorted to show desired information in unique orders or displays.

-**Credentials**: This tab sepecifies credentials by individual asset - these can be referenced by a VSA user when accessing a machine or device.

### Creating Non-Managed Assets ###

The **Demote Asset to Device** button allows you to remove a selected device as a managed asset. However, computers and mobile devices that have agents installed on them *cannot* be demoted. 

You may be asking yourself how to create non-managed assets - it's simple! Navigate to the **Discovery** module and navigate to the **Discovered Devices** page. Here, you will find a **Make Asset** button that will allow you to "promote" a device to an asset.

Discovery > Summary > Discovered Decides

! Networks can also be configured to promote devices to assets during a network scan. This is configured on the "Asset Promotion" tab within each configured network.

**Why should you use an asset?**

Routers, printers, firewalls, and other devices on networks can be detected, monitored, and reported on. Modules like Discovery, Audit, Monitor, Network Monitor, and Info Center can all be used to implement asset management on these types of agent-less devices.


- **Discovery** can detect new assets and alarm on changes to their network address.

- **Audit** allows an interface to manage these agent-less assets and store credentials.

- **Monitor and Network Monitor** can monitor these devices using various monitoring tools.

- **Info Center** provides a robust reporting tool that can provide detailed asset feedback and data for clients or management.

## Remote Access Architecture ##

### Overview ###

The Kaseya VSA delivers the fastest, most reliable remote management solution in the industry. IT professionals can access and manage computers from anywhere at near-instantaneous connect times with extraordinary reliability, even over high latency networks.

**Remote Control Objectives**

**Connect in seconds, from anywhere**: When an IT professional determines that a remote control session is required, the session must be established rapidly. The remote connection speed and reliability are critical to resolving issues quickly, maximizing IT efficiency, and retaining a happy and productive end-user.

- **Reliably connect to any environment**: As IT professionals, connecting to different IT environments and locations is the norm. Ensuring that Kaseya Remote Control is reliable in any environment is key to building the fastest and most reliable Remote Desktop Management tool. 

- **Perform well over latent or poor connections**: Latent connections are something that can not be avoided as an IT professional, especially when connecting to international endpoints. Unreliable connection performance will cost the IT professional hours of time over their many remote control sessions daily, weekly, and monthly. Kaseya Remote Control has a focus to perform well over latent connections.

! KRC utilizes **Peer-To-Peer (P2P)** connectivity whenever network conditions allow it. If the P2P connection is not possible, a **relay connection** is used instead.

### Features and Requirements ###

**Kaseya Remote Control Features**

- Supports Remote Control with or without a machine user being logged in.

- Connects to the console session by default. If an end-user is logged on, the person shares the console session with the user. Alternatively, you can connect using a private session.

- Allows you to select any additional monitors that may be running on the remote system. Support viewing multiple monitors using different resolutions.

- Supports for HiDPI Windows endpoints.

- Copies and pastes (CTRL+C and CTRL+V) plain text between local and remote systems.

- Allows for file transfer between the source machine and the remote control target, directly within the remote control application. This functionality can be triggered by dragging/dropping, copying/pasting and mouse click copy-paste functions.

- Supports the use of numerous native Windows and Apple shortcut keys on the remote machine.

- Uses the keyboard layout configured on the remote machine. Note that characters on your local keyboard might not match the characters shown on the remote user interface. You can temporarily change the keyboard layout on the remote machine to map to their local keyboard.

- Connects when a Windows machine is booted into Safe Mode with Networking.

- A log entry is created in **Agent > Agent Logs > Kaseya Remote Control** log each time a session is initiated.

### User Role and Machine Policies ###

The **User Role Policy** and the **Machine Policy** pages in the Remote Control module allow you to notify end-users that a Remote Control session to their machine is about to begin. 

Both allow the Remote Control initiator to request permission and the option to “Require admin note to start remote control” when launching the Remote Control session.

! The **Machine Policy** page takes precedence over the **User Role Policy** page. This allows you to utilize User Role Policies as the general rule across all User Roles but use the Machine Policy page to assign policies to exception endpoints.

! As a part of the File Transfer feature, a check-box "Disable Remote Control File Transfer" is available under *both* pages. By setting this option, File Transfer capabilities within Remote Control will be explicitly disabled for specific User Roles, and/or specific machines. 

This box is *exclusive* to Remote Control and does not affect file transfer capabilities of Live Connect.

**Policy Parameters**

- **Silently take control** - Take control silently and immediately without alerting the user. 

- **If user logged in display alert** - Display notification alert text. The alert text can be edited in the text box. 

- **If user logged in ask permission** - Ask the user for permission to begin a Remote Control session.

- **Require Permission. Denied if no one logged in** - Ask the user for permission to begin a remote control session.

! The ask permission text can be edited in the text box. Remote Control cannot proceed until the user clicks the "Yes" button. If nothing is clicked after one minute, "No" is assumed and the VSA removes the dialog box from the target machine. The remote control session is canceled. 

### Private Sessions and Logging ###

You can start a Kaseya Remote Control session by just clicking on the agent icon whenever this is visible in a VSA page, or via the **Quickview** window. Through the Quickview window, you can also start private Kaseya Remote Control sessions.

These private sessions enable you to connect to an endpoint, logon, and remote control the machine without accessing the console. An end-user working on the same machine at the same time cannot see your private session.

Both session types are logged to the agent log which comes in handy when tracking who accessed a machine, time-frame, length of the session, and more!

During Private Sessions, we present the following dialogue to allow for *permanent* or *temporary* configuration changes of RDP (Remote Desktop Protocol) and NLA. With this enhancement, the details of these changes are captured in the VSA Remote Control log: 

### KRC Session Logging ###

The **Remote Control log** allows you to see any recent KRC sessions and whether these were Shared or Private.

! Kaseya Remote Control logs each time someone connects to a machine. With the Reporting options, you can provide a log of the detailed Remote Control usage to authorized personnel.

### Types of Remote Control ###

*Types of Remote Control*

- **Kaseya Remote Control** : Enables you to take over the remote computer collaboratively with the end-user. You will view a shared session with the end-user or can access the managed machine through a private session. All operations are as if you were physically sitting in front of the computer.

- **Kaseya Live Connect** - Enables you to work behind the scenes without the end user’s knowledge. You will be able to fix problems in the registry, move or copy files, run a command prompt or script, view running tasks, and more. Meanwhile, the end-user is able to continue their work uninterrupted.

Remote Control and Live Connect options inside the Quickview window. You can also launch KRC by clicking the agent icon in the VSA UI.

### Launching KRC ###

Kaseya Remote Control is installed as a viewer/server pair of applications: the viewer on the administrator's local machine and the server on the remote agent machine. 

The “server” is installed as a component when a new agent is installed, or when the agent is updated using the **Agent > Update Agents** function. 

Upon clicking the agent icon, or the Remote Control button inside **Quickview**, you will be presented with this prompt and then the KRC Session. This occurs as long as it was already installed on your machine

! If the Kaseya Remote Control application is not already installed on your local machine when you start your first session, a dialog will prompt you to download and install it. Once installed, click on the agent icon to launch the remote session.  

**Recording a KRC Session**

When a KRC session has been started, select the **Record** button to initiate the recording. Once the KRC session has ended, a log will be created on this page, or you can stop the recording manually.

From there, click on any of the listed '*'.*webm* video recording files to download it, or run the file using any Kaseya supported browser.

**Paste Clipboard & Show Mouse Features**

- **Paste Clipboard**: This functionality allows the technician to paste clipboard text into password prompts using the Paste Clipboard toolbar button or Ctrl-Alt-V keyboard shortcut. The Paste Clipboard icon will be disabled if the clipboard contains no data, non-text data, or exceeds the password limit of 255 characters.

- **Show Mouse**: This functionality allows the administrator to observe the end-users mouse movements. Now the administrator mouse cursor has priority over the end-users mouse when both are using the mouse simultaneously.

### Kaseya Live Connect ###

Kaseya Live Connect is a single-machine user interface that replaces the legacy plugin-based Live Connect. The Live Connect application has been redesigned to use a Material Design look and feel. It also now runs on the local machine independent of the browser used to log into the VSA.

The **KLC** interface has a menu of tabbed property sheets that provides access to various categories of information about the managed machine.

**Kaseya Live Connect Features**

- **Custom Extensions** - This feature provides KLC users with a repository for uploading executables to the VSA. Any stored executable can be then downloaded and ran during Remote Control sessions with a single click. 

- **Filters** - Most data lists can be filtered and sorted by clicking the drop-down arrow and selecting the filter criteria.

- **Searching** - This feature provides searching capabilities where you can search registry paths in Live Connect's Registry Editor to quickly locate the registry data on an endpoint.

- **Chat** - The Chat tab allows you to communicate with the currently logged on user of the managed machine. Other VSA users can be invited to join a chat session. 

- **Mobile** - Live Connect supports connection to mobile devices such as tablets. 

## Views ##

### Overview ###

**What are Agent Views?**

Agent Views are pre-defined lists of attributes used to match against any Kaseya Agent within the Kaseya VSA interface. Using views allows a quick and efficient means of selecting and displaying a specific set of machine types. They can be applied on most pages within the VSA.

**What are Machine Filters?**

Machine filters can be applied within almost every page in the Kaseya VSA that lists Kaseya Agents, with the exclusion of the **System** module. Machine filters allow searching for an individual machine to display an individual Organization and Group within an Organization. They can be reset or removed at any time to view all agents within the VSA.

Machine filters are always in the top-left pane of the VSA next to the toolbox. Machine filters can search for any machine or display any Group/Organization.

! Agent Views and Machine Filters allow easy identification and sorting of machines. Additionally, configuration settings and policies can be easily applied to machines based on specific Agent Views.

### Machine Filters ###

Use the Machine Group filter to find endpoints that are part of a Machine Group or an Organization.

You can click the **Reset** button on your right-hand side to remove a filter. If you'd like to keep the Machine Group filter in place and search for other Machine Ids, just click the **X** next to the magnifying glass and type the new name.

### Creating and Using Basic Views ###

Agent Views are a list of settings that Kaseya VSA will verify against, making any Agent with these settings visible. These Agent Views can have pre-defined content or can be created to have specific filters or settings.

- Any number of views can be created within the Kaseya VSA.

- Agent Views can be used to identify, edit, and review machines more efficiently.

- Agent Views allows you to use the "Select All" option on a filtered set of machines that may have the same characteristics, operating system, and installed software.

**Using Predefined Views**

You can select from the many predefined views available to you in the VSA. You can switch between views or create your own.

**Creating Views**

You can create views by clicking the **+New** button followed by the **Save As** button. This will allow you to save the view and start configuring it.

The moment you click **Save As**, give your view a name, and save the changes, all the buttons from the above screenshot will no longer be grayed out.

You will see different sections inside a view including: Machine Filter, Machine Status, OS Info, Agent Procedure, Applications, Add-On Modules, Label, Patch Management, and Monitoring.

Once you're done selecting all the desired sections, click **Save** and close out the Views window to go view the agent grid.

The view will return any agents that meet the criteria you specified when creating the view.

! Since the view is set to reference a specific Machine Group, the Machine Group filter will be grayed out. You will have to clear the view itself to be able to manually select another group.

### Creating Advanced Views ###

Advanced filtering lets you design complex searches to isolate data to only the values you want. These views are created using fields that require certain unique values to be entered. Applying several Advanced Filters will refine the scope of Agents available.

The **Define Filter**... button inside the Views window.

**Advanced Views**

Advanced filtering gives you the ability to add operators combined with a desired value or a range of values as an applied filter.

Some of the operations include nested operators, AND, OR, NOT, <=, >=, and Agent Version.

## Scheduling and Executing Reports ##

### Overview ###

Once reports have been built, they can be run immediately, or on a defined schedule. 

Similar to other functions throughout the VSA, a schedule can occur either once, or it can reoccur at defined intervals.

The **Info Center > Reports** page

### Scheduling & Executing Reports ###

**Execute a report immediately**

Navigate to **Info Center > Reporting > Reports** and expand the folder where the report lives. Then, either click the **Run Now** button at the top menu bar, or right-click and select **Run Now** in the drop-down.

A report generated via **Run Now** *does not* include the built-in functionality to distribute the report to recipients.

By default, the report will include *all* managed machines (-- **All** --). Optionally, you can filter the report to a specific Organization, Machine Group, Machine Id, View, or Machine Language. 

The resulting report will include data only for machines that match the selected filter(s).

The available options after clicking **Run Now**. Whenever you specify your criteria, click **Submit** to obtain your report's output

! The data is gathered in real-time. The report is generated and will display any report parts that were included in the building of the report layout. You will be able to immediately review the returned data but note that the report is not stored for future reference.

### Schedule an individual report ###

Navigate to **Info Center > Reporting > Reports** and expand the folder where the report lives. Then, click the **Schedule** button. See the interaction below to explore the different tabs of the scheduler.

The **Schedule** tab allows you to define the recurrence and its options. As with the scheduler utility througout the VSA, the available options will vary based on whether the report is scheduled to run Once, Daily, Weekly, or Monthly. Use a recurrence to automate the distribution of reports a regular basis.

**Considerations**

- The report will run based on the *defined schedule* and will distribute to recipients based on the report configurations.

- The report *is* stored for future reference.

- The stored report can be *forwarded* to additional recipients at any time.

- If multiple reports are to be scheduled, they *must* each be scheduled *individually*, even if the recipient of all reports is the same. Use **Report Sets** to schedule multiple reports to the same recipients at one time.

### Report History ###

After the reports have been executed, you can review the historical reports. The **Schedule** page of the Info Center includes all reports and report sets published using the same scope under which you are currently logged in.  

Click the **green checkmark** icon next to the report or report set to display the history of the selected item. The **gray target** icon indicates that reports are scheduled but no history is available yet. This is common when a report is newly scheduled and has not had a chance to run yet.

**"Info Center > Schedule" page and functions**

-------------------------------------------------------------

Q: What are some examples of information collected via Audits?
A: All of the above

Q: Select all that apply: Select the three types of audit that the VSA offers.
A: Baseline Audit, Latest Audit, System Information Audit

Q: Select all that apply: Select the types of Custom Fields:
A: String, Number, Date Time, Date and Time

Q: True or False: The Managed Credentials function does not allow you to configure multiple credentials.
A: False

Q: Name a type of asset:
A: Acceptable responses: Managed Asset, Managed, Non-Managed Asset, Non-Managed Asset

Q: True or False: Kaseya Remote Control (KRC) enables you to access the remote computer collaboratively with the end-user.
A: True

Q: Select all that apply: Select all types of Remote Control:
A: Kaseya Remote Control, Private Remote Control, Kaseya Live Connect

Q: True or False: Agent Views are pre-defined lists of attributes used to match against any Kaseya Agent within the Kaseya VSA interface.
A: True

Q: True or False: Once reports have been built, they cannot be run immediately - they need a schedule first.
A: False

Q: What module/function includes all reports and report sets published?
A: Info Center > Reporting > Schedule
