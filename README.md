# osTicket — Post-Install Configuration

<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

This project picks up where the osTicket installation left off. Using both the **Admin Panel** and the **Agent Panel**, the help desk system is fully configured to simulate a real-world enterprise IT support environment. The configuration covers roles, departments, teams, agents, end-users, SLA plans, and help topics — creating a structured, policy-driven ticketing workflow.


> **Prerequisite:** This project is built on top of the osTicket installation completed in Part 1:
> [osTicket — Prerequisites and Installation](https://github.com/solomonyohanis/osticket-prerequisites-and-installation)

---

## Environments and Technologies Used

- Windows 10 (Virtual Machine)
- Internet Information Services (IIS)
- osTicket v1.18
- File Explorer (Windows)

## Operating System

- Windows 10 Pro (Virtual Machine running locally via IIS)

---

## osTicket Portal URLs

| Portal | URL | Purpose |
|---|---|---|
| **Admin / Agent Login** | `http://localhost/osTicket/scp/login.php` | Staff portal — agents and admins log in here to manage and resolve tickets |
| **End User Portal** | `http://localhost/osTicket` | Public help desk — customers submit and track tickets here |

---

## Post-Install Configuration Steps

1. [Configure Roles](#step-1--configure-roles)
2. [Configure Departments](#step-2--configure-departments)
3. [Configure Teams](#step-3--configure-teams)
4. [Secure the Installation](#step-4--secure-the-installation)
5. [Configure Agents](#step-5--configure-agents)
6. [Configure Users (Customers)](#step-6--configure-users-customers)
7. [Configure SLA Plans](#step-7--configure-sla-plans)
8. [Configure Help Topics](#step-8--configure-help-topics)

---

## Step 1 — Configure Roles

**Admin Panel → Agents → Roles**

> **What is a Role?**
> Roles are permission bundles assigned to agents. Instead of giving every agent full admin access, roles let you define exactly what an agent can do — such as viewing tickets, closing them, deleting them, assigning them to other agents, and so on. A role does not represent a job title; it controls what actions are available inside osTicket.

<img width="1920" height="955" alt="01_agent_login" src="https://github.com/user-attachments/assets/5ec501e9-d19e-4813-b150-d67e6748adb4" />

To begin, navigate to `http://localhost/osTicket/scp/login.php` and log in with the **adminuser** account created during installation.

<img width="1920" height="955" alt="02_staff_control_panel_open_tickets" src="https://github.com/user-attachments/assets/c5fb906d-4312-4433-9c45-404538b91c32" />

After logging in, the **Staff Control Panel** displays. This is where agents work day-to-day. To access admin settings, click **Admin Panel** in the top-right corner.

<img width="1920" height="955" alt="03_admin_panel_system_logs" src="https://github.com/user-attachments/assets/1fbf37ff-9770-448f-8ada-da28fd84eb88" />

You are now in the **Admin Panel**. This area controls all system-level settings. You can confirm you are in the Admin Panel because the top-right corner now shows "Agent Panel" as the link to switch back.

<img width="1920" height="955" alt="04_admin_agents_dropdown_menu" src="https://github.com/user-attachments/assets/07dbdd8d-5100-4dde-8fc7-c07857659e10" />

Click the **Agents** tab in the top navigation bar to reveal a dropdown with four options: **Agents**, **Teams**, **Roles**, and **Departments**. Click **Roles**.

<img width="1920" height="955" alt="05_roles_list_existing" src="https://github.com/user-attachments/assets/f852ae87-d3d6-41df-ac7b-fcbc48e78298" />

The Roles page shows roles that were created during installation: **All Access**, **Expanded Access**, **Limited Access**, and **View only**. A new role with full permissions will be added here.

<img width="1920" height="955" alt="06_roles_list_highlight_add_new" src="https://github.com/user-attachments/assets/a57e3d5c-343f-48e1-a6cd-7d780eafcac1" />

Click the **Add New Role** button (highlighted in green) in the top-right of the Roles page.

<img width="1920" height="955" alt="07_add_new_role_definition_supreme_admins" src="https://github.com/user-attachments/assets/16c3ed53-2374-4cce-8442-197837462b48" />

In the **Definition** tab, enter the name **Supreme Admins** in the Name field. This role will be granted every available permission in osTicket. Click the **Permissions** tab to continue.

> **Why "Supreme Admins"?**
> This is a demonstration role representing the highest level of access. In a real environment, you would name roles based on your team structure (e.g., "Tier 2 Support", "Senior Analyst").

<img width="1920" height="955" alt="08_permissions_tickets_unchecked" src="https://github.com/user-attachments/assets/0de4e1cf-3e3e-4bba-ace3-03c4237c91e6" />

The Permissions tab has three sub-sections: **Tickets**, **Tasks**, and **Knowledgebase**. Each lists specific capabilities that can be toggled on or off. Currently all boxes are unchecked.

<img width="1920" height="955" alt="09_permissions_tickets_all_checked" src="https://github.com/user-attachments/assets/9b6581ba-3def-46eb-aea8-6059ddfb9483" />

Check every box in the **Tickets** sub-tab. These permissions include: Assign, Close, Create, Delete, Edit, Edit Thread, Link, Mark as Answered, Merge, Post Reply, Refer, Release, and Transfer.

<img width="1920" height="955" alt="10_permissions_tasks_all_checked" src="https://github.com/user-attachments/assets/971d4d94-3b41-48d9-91e0-c72728f7cbae" />

Switch to the **Tasks** sub-tab and check all boxes there as well: Assign, Close, Create, Delete, Edit, Post Reply, and Transfer. Click **Add Role** to save.

<img width="1920" height="955" alt="11_roles_list_supreme_admins_added" src="https://github.com/user-attachments/assets/31d27fa1-f0a5-46c8-8d20-e58a404a5a81" />

A green success banner confirms the role was created. **Supreme Admins** now appears in the Roles list alongside the existing roles.

---

## Step 2 — Configure Departments

**Admin Panel → Agents → Departments**

> **What is a Department?**
> Departments are the primary organizational units in osTicket. They control which agents see which tickets. Every ticket must belong to a department, and agents are assigned to one primary department. Examples: IT Support, Billing, HR, Networking. Departments can be set as **Top-Level** (standalone) or nested under a parent department.

<img width="1920" height="955" alt="12_departments_list_existing" src="https://github.com/user-attachments/assets/326fda26-fbf2-4a62-a554-81393342a990" />

Click **Departments** under the Agents tab. Three departments already exist from installation: **Maintenance**, **Sales**, and **Support** (the default). A new department for system administrators will be added.

<img width="1920" height="955" alt="13_add_new_department_form_empty" src="https://github.com/user-attachments/assets/364ca1f4-969c-4652-8e63-5dd083b950b3" />

Click **Add New Department**. The settings form includes options for parent department, type (Public or Private), SLA plan, manager, and email routing.

<img width="1920" height="955" alt="14_add_new_department_system_administrators" src="https://github.com/user-attachments/assets/56e8faec-7080-4762-86c7-a0a1171e7495" />

Enter **System Administrators** as the department name. Leave the parent as **Top-Level Department** and the type as **Public**. Scroll down to see the Create Dept button.

<img width="1920" height="955" alt="15_department_form_bottom_create_dept" src="https://github.com/user-attachments/assets/85c6453b-5de2-4961-a79c-6dc1344fd589" />

Scroll to the bottom of the form and click **Create Dept** to save the new department.

<img width="1920" height="955" alt="16_departments_list_system_administrators_added" src="https://github.com/user-attachments/assets/5fc27384-860c-43cb-aba0-d8f65da4e315" />

A green success banner confirms the creation. **System Administrators** now appears in the Departments list.

---

## Step 3 — Configure Teams

**Admin Panel → Agents → Teams**

> **What is a Team?**
> While departments are fixed organizational groups, teams are flexible cross-departmental groups. A team can pull agents from any department together for a specific purpose — for example, a "Critical Outage Response" team might include agents from Networking, Desktop Support, and Server Admins. Agents on a team can access tickets assigned to that team regardless of their home department.

<img width="1920" height="955" alt="17_teams_list_level_i_support" src="https://github.com/user-attachments/assets/c10e2c37-969f-4f78-bdb8-47997b9eebfc" />

The Teams page shows **Level I Support** created during installation. A second team, Level II Support, will now be added.

<img width="1920" height="955" alt="18_delete_setup_folde" src="https://github.com/user-attachments/assets/c9881d65-7844-4d84-9486-2221defbcc48" />

> **Security Step — Delete the Setup Folder**
> Before continuing, the `setup` folder inside `C:\inetpub\wwwroot\osTicket\` must be deleted. This folder was only needed during installation. Leaving it in place is a security risk because anyone could revisit the installation wizard and overwrite your configuration. Right-click the **setup** folder and click **Delete**.

<img width="1920" height="955" alt="19_add_new_team_form_empty" src="https://github.com/user-attachments/assets/a20358da-c4ee-4318-9ce4-993b37a324cc" />

Back in the Admin Panel, go to **Agents → Teams** and click **Add New Team**.

> Notice the yellow banner now says **"Please change permission of config file (ost-config.php) to remove write access"** — this is addressed in the next security step.

<img width="1920" height="955" alt="20_ost_config_advanced_security_full_control" src="https://github.com/user-attachments/assets/d2b7ab76-d6e2-405e-9b63-b7ded3a480c8" />

> **Security Step — Lock Down ost-config.php**
> Navigate to `C:\inetpub\wwwroot\osTicket\include\` and right-click **ost-config.php → Properties → Security → Advanced**. The file currently grants **Everyone: Full control**, which means anyone could modify the configuration file.

<img width="1920" height="955" alt="21_ost_config_permission_entry_read_only" src="https://github.com/user-attachments/assets/3e018974-cda0-48cb-8d1e-0cae02f16dbf" />

Click **Edit** on the Everyone permission entry. Uncheck everything except **Read**, then click OK.

<img width="1920" height="955" alt="22_ost_config_advanced_security_read_confirmed" src="https://github.com/user-attachments/assets/41618529-d385-4a87-af64-1deab31640fe" />

The Advanced Security Settings now shows **Everyone: Read** — the file is now read-only. The yellow warning banner in osTicket will disappear after refreshing.

<img width="1920" height="955" alt="23_add_new_team_name_level_ii_support" src="https://github.com/user-attachments/assets/a9c4ce70-ec55-4d9a-93f3-5d27b6eba44d" />

Enter **Level II Support** in the Name field and click **Create Team**.

<img width="1920" height="955" alt="24_team_level_ii_support_added_success" src="https://github.com/user-attachments/assets/2c9f8101-7466-4141-adc4-cbfe4aeb2928" />

The team is successfully created and the page becomes **Update Team — Level II Support**.

<img width="1920" height="955" alt="25_teams_list_level_i_and_ii" src="https://github.com/user-attachments/assets/74fbbb9f-ca4d-4a43-835e-89ab64fa828f" />

The Teams list now shows both **Level I Support** and **Level II Support**.

---

## Step 4 — Secure the Installation

The two security tasks above — deleting the `setup` folder and making `ost-config.php` read-only — are both completed at this stage. These steps protect your osTicket installation from being tampered with or reinstalled after it is live.

---

## Step 5 — Configure Agents

**Admin Panel → Agents → Agents**

> **What is an Agent?**
> Agents are the staff members (support reps, IT technicians, help desk analysts) who log into the osTicket staff panel to work on tickets. Each agent is assigned to a primary department and a role, which together determine what tickets they see and what actions they can take.

<img width="1920" height="955" alt="26_agents_list_solomon_only" src="https://github.com/user-attachments/assets/3a7a3c10-1f5b-4dc5-b8d4-01ab9f67a084" />

The Agents list currently shows only **Solomon Yohanis** (the admin account). Two new agents will be added.

<img width="1920" height="955" alt="27_add_new_agent_form_empty" src="https://github.com/user-attachments/assets/a6fe476f-c82f-4f04-a3a7-8c73b8f3ed71" />

Click **Add New Agent**. The Account tab collects the agent's name, email, username, and password settings.

<img width="1920" height="955" alt="28_add_new_agent_jane_dao_account" src="https://github.com/user-attachments/assets/5bc0f6ea-afc5-4e33-9437-2def3978bc64" />

**Agent 1 — Jane Dao**

Fill in:
- **Name:** Jane Dao
- **Email:** janedao@gmail.com
- **Username:** jane_dao

Click **Set Password** to assign a password, then navigate to the **Access** tab.

<img width="1920" height="955" alt="29_jane_dao_access_tab_empty" src="https://github.com/user-attachments/assets/ada4389a-b520-45d0-afff-b92c01136deb" />

The **Access** tab sets the agent's primary department and role. The **Primary Department** determines which tickets the agent can see by default.

<img width="1920" height="955" alt="30_jane_dao_access_support_limited_access" src="https://github.com/user-attachments/assets/4247ca6f-617e-4d8c-b49a-581f464df044" />

Set Jane Dao's Primary Department to **Support** and her Role to **Limited Access**. This restricts Jane to the support queue with a limited set of actions.

<img width="1920" height="955" alt="31_jane_dao_teams_level_i_support" src="https://github.com/user-attachments/assets/f280a12e-8060-4541-a711-63479ebd3839" />

Click the **Teams** tab and select **Level I Support** from the dropdown. Click **Create** to save the agent.

<img width="1920" height="955" alt="32_jane_dao_successfully_added" src="https://github.com/user-attachments/assets/944d018f-2a0e-4060-acb3-a60c1a4bb304" />

Jane Dao is successfully added. The page becomes **Manage Agent — Jane Dao**.

<img width="1920" height="955" alt="33_agents_list_jane_and_solomon" src="https://github.com/user-attachments/assets/3416f80e-fdc4-48af-8409-f0651411a0fe" />

The Agents list now shows **Jane Dao** and **Solomon Yohanis**.

<img width="1920" height="955" alt="34_add_new_agent_thomas_smith_account" src="https://github.com/user-attachments/assets/1bf12e6d-6fcf-415f-89c8-c3b4cbaf6c27" />

**Agent 2 — Thomas Smith**

Fill in:
- **Name:** Thomas Smith
- **Email:** thomassmith@gmail.com
- **Username:** thomas_smith
- Check **"Limit ticket access to ONLY assigned tickets"** — this restricts Thomas to only seeing tickets explicitly assigned to him, useful for contractors or junior staff.

<img width="1920" height="955" alt="35_thomas_smith_access_support_expanded" src="https://github.com/user-attachments/assets/1811bc10-eeec-46ec-b7a5-210871162662" />

Set Thomas Smith's Primary Department to **Support** and his Role to **Expanded Access**, giving him more ticket actions than Jane but still less than a Supreme Admin.

<img width="1920" height="955" alt="36_thomas_smith_teams_level_ii_support" src="https://github.com/user-attachments/assets/e65c0320-8f8b-45ef-aa1b-8e4b5534b3e6" />

Assign Thomas to **Level II Support** on the Teams tab, then click **Create**.

<img width="1920" height="955" alt="37_thomas_smith_successfully_added" src="https://github.com/user-attachments/assets/e98bf30b-fab8-44c3-94a3-8bbf687d6364" />

Thomas Smith is successfully created.

<img width="1920" height="955" alt="38_agents_list_all_three" src="https://github.com/user-attachments/assets/dfbc73fb-6800-42bf-89a7-2dff147297bf" />

The Agents list now shows all three agents: **Jane Dao**, **Solomon Yohanis**, and **Thomas Smith**.

---

## Step 6 — Configure Users (Customers)

**Agent Panel → Users → User Directory**

> **What is a User?**
> Users are the end-customers who submit support tickets. Unlike agents, users do not have access to the admin or staff panel — they interact with osTicket only through the public-facing end-user portal. Users can be registered (with accounts) or guests (email only). The User Directory in the Agent Panel lets staff manage and look up user accounts.

> **Note:** To configure users, you must switch from the Admin Panel to the **Agent Panel** by clicking "Agent Panel" in the top-right corner.

<img width="1920" height="955" alt="39_user_directory_osticket_team_only" src="https://github.com/user-attachments/assets/05cc2cb2-5a49-406c-9db2-b489f2549393" />

Navigate to the **Agent Panel → Users → User Directory**. Only the default osTicket Team account exists. A new end-user will be added.

<img width="1920" height="955" alt="40_add_user_modal_empty" src="https://github.com/user-attachments/assets/aa18e868-60e3-40bd-a5a2-f8da9e602b70" />

Click **Add User**. A modal dialog appears with a search bar (to look up existing users) and a form to create a new one.

<img width="1920" height="955" alt="41_add_user_karen_gmail" src="https://github.com/user-attachments/assets/fc5c9cf4-5f81-4082-b3a6-82839178a487" />

Fill in:
- **Email:** karen@gmail.com
- **Full Name:** Karen

Click **Add User**.

<img width="1920" height="955" alt="42_karen_user_profile_created" src="https://github.com/user-attachments/assets/77e85e54-9736-4655-9ad0-12f03eb3223e" />

Karen's user profile is created. Her status is **Guest**, which means she can submit tickets by email without a full registered account. The **Register** button would allow giving her a login if needed.

<img width="1920" height="955" alt="43_user_directory_karen_and_osticket_team" src="https://github.com/user-attachments/assets/43a316d9-b332-4568-a5ef-8e82777cac5a" />

The User Directory now shows **Karen** alongside the osTicket Team default user.

---

## Step 7 — Configure SLA Plans

**Admin Panel → Manage → SLA**

> **What is an SLA Plan?**
> SLA stands for **Service Level Agreement**. In osTicket, an SLA Plan defines how quickly a ticket must be addressed before it is marked **overdue**. The SLA plan sets a **grace period** (in hours) and a **schedule** (24/7 or business hours only). When a ticket is created, it is automatically assigned to an SLA based on its help topic or department, and the clock starts ticking.

<img width="1920" height="955" alt="44_sla_list_default_sla" src="https://github.com/user-attachments/assets/79bf6ec2-775b-44b1-ab05-cd4d2d42e077" />

Navigate to **Admin Panel → Manage → SLA**. Only the **Default SLA** (18-hour grace period) exists. Three new SLA tiers will be added.

<img width="1920" height="955" alt="45_add_new_sla_plan_form_empty" src="https://github.com/user-attachments/assets/93ba3c01-e822-49ea-8053-7eb2f59a0603" />

Click **Add New SLA Plan**. The form collects the plan name, grace period (in hours), and schedule.

<img width="1920" height="955" alt="46_sla_sev_a_1hr_24_7" src="https://github.com/user-attachments/assets/2aae0001-78c2-47ab-b3d3-2b06a892461f" />

**Sev-A** — The highest-priority SLA:
- **Grace Period:** 1 hour
- **Schedule:** 24/7

This means a Sev-A ticket must receive a response within 1 hour, at any time of day or night, including weekends and holidays.

<img width="1920" height="955" alt="47_sla_list_sev_a_added" src="https://github.com/user-attachments/assets/1e2ce881-85ad-4b71-aa23-b36e77240dea" />

Sev-A is added. Now add Sev-B.

<img width="1920" height="955" alt="48_sla_list_sev_b_added" src="https://github.com/user-attachments/assets/98546549-e2de-4750-adff-a15769c67da1" />

**Sev-B** — Medium-priority:
- **Grace Period:** 4 hours
- **Schedule:** 24/7

Sev-B tickets require a 4-hour response window around the clock.

<img width="1920" height="955" alt="49_sla_sev_c_8hr_business_hours" src="https://github.com/user-attachments/assets/482fd5cb-b815-4d16-b370-3040524dcf16" />

**Sev-C** — Standard priority:
- **Grace Period:** 8 hours
- **Schedule:** Monday–Friday, 8am–5pm (with U.S. Holidays)

Sev-C tickets only count time during business hours. An 8-hour grace period on a Friday evening would not expire until Monday morning.

<img width="1920" height="955" alt="50_sla_list_all_three_sev_a_b_c" src="https://github.com/user-attachments/assets/3304e26d-23af-4e52-96f3-e0ec32000c55" />

All three SLA plans — **Sev-A**, **Sev-B**, and **Sev-C** — are now listed alongside the Default SLA.

---

## Step 8 — Configure Help Topics

**Admin Panel → Manage → Help Topics**

> **What is a Help Topic?**
> Help Topics are the categories users select when submitting a ticket (e.g., "Password Reset", "Equipment Request", "Report a Problem"). They serve as the entry point for routing: based on the help topic chosen, osTicket can automatically assign the ticket to a specific department, apply an SLA plan, set a priority level, and auto-assign it to an agent. Help Topics make the system self-routing.

<img width="1920" height="955" alt="51_help_topics_list_existing_four" src="https://github.com/user-attachments/assets/66196e8d-be86-4202-8358-a3249064365d" />

Navigate to **Admin Panel → Manage → Help Topics**. Four help topics already exist: **Feedback**, **General Inquiry**, **Report a Problem**, and **Report a Problem / Access Issue**.

<img width="1920" height="955" alt="52_add_new_help_topic_form_empty" src="https://github.com/user-attachments/assets/de53ddb2-00f5-4700-9698-4948dafa5795" />

Click **Add New Help Topic**. The form has a **Help Topic Information** tab (name, type, parent topic) and a **New ticket options** tab (for routing configuration).

<img width="1920" height="955" alt="53_add_new_help_topic_business_critical_outage" src="https://github.com/user-attachments/assets/bc154e8b-3baa-40cf-a5e5-b02bd1149e70" />

**Topic 1 — Business Critical Outage**

- **Topic:** Business Critical Outage
- **Parent Topic:** Report a Problem

This nests the new topic under "Report a Problem" so users see it as a sub-category when submitting tickets.

<img width="1920" height="955" alt="54_help_topics_list_five_topics" src="https://github.com/user-attachments/assets/b57cf6c1-8c11-4dd9-acfb-b176b5a461d9" />

Business Critical Outage appears in the list as **Report a Problem / Business Critical Outage**, showing its parent-child relationship.

<img width="1920" height="955" alt="55_password_reset_successfully_added" src="https://github.com/user-attachments/assets/0f2fd93a-976b-4daa-8fde-81ef3f41516b" />

**Topic 2 — Password Reset**

Added as a top-level topic. Password resets are one of the most common IT help desk requests and warrant their own category for fast routing.

<img width="1920" height="955" alt="56_personal_computer_issues_successfully_added" src="https://github.com/user-attachments/assets/31cc4df2-3946-4d57-b503-509aeb54f1ba" />

**Topic 3 — Personal Computer Issues**

Also added as a top-level topic. This covers hardware, software, and general workstation problems.

<img width="1920" height="955" alt="57_help_topics_final_list_all_eight" src="https://github.com/user-attachments/assets/32ee299d-e63f-440a-9f69-816364592dd0" />

The Help Topics list now contains all eight topics: **Equipment Request**, **Feedback**, **General Inquiry**, **Password Reset**, **Personal Computer Issues**, **Report a Problem**, **Report a Problem / Access Issue**, and **Report a Problem / Business Critical Outage**.

<img width="1920" height="955" alt="58_business_critical_outage_new_ticket_options_empty" src="https://github.com/user-attachments/assets/6888a589-dfc2-4abd-83c8-16b7f927f071" />

Clicking on **Report a Problem / Business Critical Outage** and navigating to the **New ticket options** tab shows the routing configuration. Here you can tie the help topic to a specific department, SLA plan, priority, and auto-assign agent.

<img width="1920" height="955" alt="59_business_critical_outage_routing_configured" src="https://github.com/user-attachments/assets/65ffea86-9a40-4bcb-b6b5-0c79a3feb823" />

The routing for Business Critical Outage is configured:
- **Department:** System Administrators
- **Status:** Open
- **Priority:** Emergency
- **SLA Plan:** Sev-A (1 hour — Active)
- **Auto-assign To:** Solomon Yohanis

This means any ticket submitted under "Business Critical Outage" will automatically be routed to the System Administrators department, flagged as Emergency, assigned the strictest SLA (1-hour response), and auto-assigned to the lead admin.

<img width="1920" height="955" alt="60_help_topics_final_list_emergency_confirmed" src="https://github.com/user-attachments/assets/51f1e817-2d49-4b0e-89c9-5f2abfba0256" />

The Help Topics list confirms the update — **Report a Problem / Business Critical Outage** now shows **Emergency** priority and **System Administrators** as its department.

---

## Summary

This configuration transforms a freshly installed osTicket instance into a fully functional enterprise help desk system. The table below summarizes everything configured:

| Component | Items Created |
|---|---|
| **Roles** | Supreme Admins (all permissions) |
| **Departments** | System Administrators |
| **Teams** | Level II Support |
| **Agents** | Jane Dao (Support / Limited Access / Level I), Thomas Smith (Support / Expanded Access / Level II) |
| **Users** | Karen (karen@gmail.com) |
| **SLA Plans** | Sev-A (1 hr / 24-7), Sev-B (4 hrs / 24-7), Sev-C (8 hrs / Business Hours) |
| **Help Topics** | Business Critical Outage, Password Reset, Personal Computer Issues, Equipment Request |
| **Security** | Setup folder deleted, ost-config.php set to Read-only |

The system is now ready for the next phase: **Ticket Lifecycle Practice** — creating, triaging, assigning, and resolving tickets as both an agent and an end-user.
