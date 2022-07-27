# What can Kaseya Automate?

- By automating simple tasks such as device discovery and information collection
	- Locate a computer

	- Create a standard local admin account

	- Add a computer to the domain

	- Install all missing patches

	- Configure monitoring

	- Collect device hardware and software information

	- Notify management of status

- check into the Kaseya Server regardless of the network as long as port 5721 is open.
- In addition to computers, network devices such as printers, routers, and switches can be monitored, even without an agent. 

- On Prem requires Kaseya  Server & thd SQL Database server
- The database ksubscribers stores all data associated with the Virtual System Administrator (VSA), including users and access rights, agent records and settings, agent procedures, policies, etc. 

## User Preferences
- First Function and Compact Navigation
- There are three options on this page that apply to all users and only display for master role users: Setting the "System Default Language Preference", the "Download" button for installing language packs, and "Show shared and private folder contents from all users". 
 ---

## Creating Organizations
- Navigate to System > Orgs/Groups/Depts/Staff > Manage.

! You cannot have Machine Groups belonging to multiple Organizations; it's a 1:1 relationship.

## Creating  Machine Groups

- Following Organizations, Machine Groups are the bottom-level containers for Agents. Agents are always defined by a Machine Group.

- You can define multi-level hierarchies of Machine Groups by identifying a parent-level group for a Machine Group. 

! You cannot have agents belonging to multiple Machine Groups; it's a 1:1 relationship.

---

## User Roles & Scopes

- The Kaseya VSA has two options to control the security in the VSA.

- You can find these functions in your VSA under the System module. 

- Roles dictate what actions a VSA user can perform

- Scopes dictate what a VSA user can see
 
---

Q. What module/function allows you to set system-wide preferences?

A. System > User Settings > Preferences

Q. True or False: A Machine Group is the top-level container in the VSA.

A. False

Q. True or False: You cannot have agents belonging to multiple Machine Groups.

A. True

Q. True or False: Roles dictate what actions a user can perform inside the VSA while Scopes dictate which machines a user can see.

A. True
